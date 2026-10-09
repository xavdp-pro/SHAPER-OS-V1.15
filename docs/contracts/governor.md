# Governor Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

The governor owns a durable desired-state ledger in its own private MariaDB. It writes what should exist, derives work from the gap and records what enrolled makers report. It never opens a command channel to a host and holds no host key. Its product identity is irrelevant to the maker.

## Invariants

1. **Govern by writing.** Makers poll for work; the governor never pushes commands. State, enrollment, refusal and retry evidence survives restart. The constructor generates the implementation and database adapter from this contract.
2. <a id="identity-is-the-host"></a>**Identity is the host.** Tandem enrollment binds one credential to the actual hostname and its optional human-facing `fleetName`. Bind those names once; a row's machine may name either bound value. Refuse polls claiming another host and reports on another machine's row. Journal each known-credential refusal with who, row, machine, event and time; do not cap or coalesce repeated security facts. An unknown token receives 401 and does not populate that enrolled-maker journal. Repeated misuse requires the tandem's revocation, not silent log reduction. Enrollment is not self-service.
3. **No work for unproven bytes.** Each poll advertises the matrices actually held by digest. Withhold work requiring an absent digest and return a preload instruction. Verify the artifact bytes, not just its filename. Adoption is the explicit exception because it creates no new runtime.
4. <a id="one-live-row"></a>**One live row per account/class.** Repeated desire is idempotent. A re-ask for a `DEGRADED` dev/test/demo row makes its deadline now and creates one successor; repetition never creates twins. A production re-ask is refused as a typed result carrying the existing row ID, and its slot remains held until an authorized human/root termination is independently observed. Do not invent an undocumented release endpoint; any added administrative operation has an explicit local contract and authority.
5. **Poll is heartbeat.** Date each poll. Silence beyond the declared interval is drift with an out-of-band alarm, never a healthy tile.
6. <a id="deadlines-are-desired-state"></a>**Deadlines and repair are bounded.** A past-deadline row yields reap, never stamp, even if it was never born; the recipe proves absence. Failed reaps use exponential backoff (default initial 30 seconds) and stop at `maxHealingAttempts` (default 5), leaving `DEGRADED` and alerting. `REAP_REFUSED` is a separate terminal refusal for automation and is never offered repeatedly. A silent claim becomes eligible for reconciliation after `claimBudgetMs` (default ten minutes); persist its attempt count and apply the same bounded-repair obligation before re-offering. Reconcile any possible prior effect before retry. The constructor implements bounded claims explicitly rather than preserving an endless retry gap.
7. **Isolated, durable ownership.** Keep the core independent of a product and avoid unnecessary dependencies. Language/runtime choices are not universal law. The real governor binds its own private database; an in-memory test store or JSONL fixture does not satisfy deployment durability.
8. <a id="a-birth-is-a-fact"></a>**A birth is observed.** `STAMPED` requires `data.state` equal to `running`, case-insensitively; absent or stopped facts yield `DEGRADED` and identify the unmet fact. `ADOPTED` additionally requires `data.legacy: true`. The event name or a zero exit code alone is insufficient.
9. <a id="params-are-typed"></a>**Params are typed, allow-listed, immutable and unique.** `params` is a flat object of strings, numbers or booleans under keys matching `^[a-z][a-z0-9_]{0,31}$`. The product declares each class's `paramsSchema` with type and optional `unique`. Reject unknown keys, wrong types or undeclared params as typed facts naming the key. No declaration means no params. A re-ask with changed params is refused with the existing row ID. A unique value is held by only one live class row; a conflict identifies its holder. `REAPED` releases it. For degraded handover, the successor can reserve the same value, but its birth is returned as a typed `withheld` entry naming the predecessor until the predecessor is actually `REAPED`. The product allocates values before desire; the governor enforces uniqueness. Params travel beside the six typed arguments, then as `SHAPER_PARAM_<KEY>` in a fresh allow-listed recipe environment, never shell text, inherited process environment or a seventh argument.
10. <a id="an-adopted-row-creates-nothing"></a>**Adoption creates nothing.** An adopted row declares `matrix: "none"` and `digest: "none"` literally, not omitted, and names the existing container through its class-declared unique `instance` param. Refuse a nameless adoption. `adopt` is not inventory-gated or preloaded. It reports observed running state and `legacy: true`; failure degrades. The `none` digest never pins a matrix. Adoption creates/launches nothing and never executes inside the target. Before enabling it for a host family, qualify adopt, reap and validate against `SHAPER_PARAM_INSTANCE`; no recipe may accidentally act on a name derived from row ID instead. Report `checks: true` only when that validation path is actually supported.

## Ledger fields and states

Each instance row contains `id`, `account`, `klass`, `matrix`, `digest`, `machine`, `env`, `state`, `params`, `deadlineAt`, `createdAt`, `updatedAt`, `events[]`. `env` is `dev`, `test`, `demo` or `prod`; absent means `demo`, never production. Artifact digest and params remain immutable on a live row. The backup bucket is derivable, not an alternate instance store.

The states are exactly `DESIRED`, `RECONCILING`, `PURRING`, `DEGRADED`, `REAPED`. Unknown event names are retained for audit but cause no transition. Every report records event, data, maker host and timestamp. Apply a transition only to the current authorized work kind and correlated claim/attempt, from an eligible source state below. Stale, mismatched or ineligible reports remain audit evidence without changing state; duplicate reports cannot repeat a settled transition. The realization declares and persists the attempt correlation and transition guards.

| Event | Eligible source state and work | Next state |
| :--- | :--- | :--- |
| `STAMPING` | `DESIRED`; current stamp claim | `RECONCILING` |
| `STAMPED` | `DESIRED` or `RECONCILING`; current stamp attempt | `PURRING`, only with required running facts |
| `STAMP_FAILED` | `DESIRED` or `RECONCILING`; current stamp attempt | `DEGRADED` |
| `REAPING` | Nonterminal row eligible for authorized reap under the deadline/recovery policy | `RECONCILING` |
| `REAPED` | Current authorized reap attempt on a nonterminal row | `REAPED`, after verified absence |
| `REAP_FAILED` | Current reap attempt on a nonterminal row | `DEGRADED`, bounded retry policy applies |
| `REAP_REFUSED` | Current reap attempt on a nonterminal row | `DEGRADED`, no automatic reap re-offer |
| `VALIDATING` | `PURRING`; current validation attempt | `PURRING` (progress alone does not assert success or failure) |
| `VALIDATED` | `PURRING`; same validation attempt | `PURRING` |
| `VALIDATION_FAILED` | `PURRING`; current validation attempt | `DEGRADED` |
| `ADOPTING` | `DESIRED`; current adoption claim | `RECONCILING` |
| `ADOPTED` | `DESIRED` or `RECONCILING`; current adoption attempt | `PURRING`, only with running and legacy facts |
| `ADOPT_FAILED` | `DESIRED` or `RECONCILING`; current adoption attempt | `DEGRADED` |

A correlated terminal birth report does not require prior delivery of its
progress event; required running/legacy facts still apply. For an eligible birth
report, unmet required facts override the claimed healthy
transition to `DEGRADED`. `REAPED` is terminal: late progress, validation or birth
reports never resurrect its row. Authorized human/root termination follows its
declared administrative contract and the same independently verified absence.

Distinguish an explicitly permitted bounded recovery from a resting
`DEGRADED` row. Persist the cause, current recovery phase, attempt count and
eligibility. Admission of an authorized bounded retry explicitly records
`RECONCILING` before execution; a report alone cannot admit a retry from rest.
In particular, a failed reap may be re-offered under the existing
backoff and remaining budget; an exhausted budget or `REAP_REFUSED` does not
become eligible merely because another poll or report arrives. A diagnostic
validation of a resting row is evidence only: it neither clears `DEGRADED`
nor starts another repair budget. Leaving rest requires the documented re-ask
where permitted or authorized human/root action under
[Rule 27](../../RULES.md#rule-27); the event table grants no additional recovery authority.

`PURRING` is dated; the canonical instance `status.json` exposes state, `lastPurr` and `lastBackup`. Staleness triggers observation. A DEGRADED row does not silently self-clear; only the documented bounded recovery, explicit re-ask where permitted or authorized human/root action can change it.

## Exact HTTP door

Bearer authorization applies to these exact routes; arbitrary paths below `/api/work/` are not report endpoints.

| Request | Required behavior |
| :--- | :--- |
| `POST /api/makers/enrol` | Operator/admin credential; body `host`, optional `fleetName`. Return created enrollment (201); invalid/duplicate binding 400; unauthorized 401 |
| `POST /api/makers/poll` | Maker credential; body `host`, `version`, `lanes`, `inventory` (digest list). Return 200 with `ok`, `work`, `preload`, `withheld`, or explicit refusal status |
| `POST /api/work/<rowId>/events` | Bound maker credential; body `event`, `data`. Return `ok`, resulting `state` and `unmet` if facts fail; unknown token 401, missing row 404, wrong machine 403 |
| Any other route | 404 |

Each work item contains `workId` (`<kind>:<rowId>`), `kind`, `rowId`, `klass`, `matrix`, `digest`, `account`, `env`, `params`. The four kinds are `stamp`, `reap`, `validate`, `adopt`. Respect the maker's declared lane count. Claim and result correlation survives retry/restart.

The HTTP door and core remain separable so an application can mount the same contract without acquiring host power. Administrative desire/list/revocation and any new operation are explicitly described in its realization, never inferred from a guessed path.

Read [maker](maker.md), [typed recipes](maker-recipes.md), [fleet](../architecture/FLEET.md), [lexicon](../architecture/LEXICON.md) and [Rules 23, 27, 36 and 37](../../RULES.md).
