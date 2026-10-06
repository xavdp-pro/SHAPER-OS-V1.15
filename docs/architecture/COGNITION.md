# Cognition Requirements

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

[Rules 0H, 7 and 21](../../RULES.md) bind this capability declaration and measured selection contract. The constructor implements any routing needed in the realization; this document does not claim a router ships in the OS.

## Why this exists

Model capability moves. In six months the fastest engine, the cheapest engine and
the strongest engine will all be different products. A system that hardcodes
*which model* is obsolete on that day; a system that declares *what the work
requires* is not.

So a brick never says "use model X". It says: **this is the reasoning depth my
work needs, this is the throughput order of magnitude it needs, and this is what
I do when neither is available.** Matching requirement to engine is a separate,
replaceable decision.

---

## Axis 1 — Capacity class (what kind of work)

Rule 21's existing vocabulary. Unchanged, vendor-agnostic:

| Class | Work |
| :--- | :--- |
| `heavy-engineering` | High-reasoning architecture, multi-file refactoring, autonomous code generation |
| `rapid-iteration-ui` | Interactive GUI components, visual refinement |
| `infra-ops` | Vulnerability scans, system administration, container orchestration |
| `fast-eval` | Streaming acknowledgments, low-latency text classification |

A class whose engine needs a human at the keyboard is declared `interactive: true`
and is never auto-dispatched (Rule 21).

## Axis 2 — Reasoning depth (how much intelligence)

| Depth | The work requires | Typical of |
| :--- | :--- | :--- |
| `D0` | No model at all. Deterministic code. | Health probes, checksum verification, boot order |
| `D1` | Literal transformation: extract, classify, format, follow an unambiguous step | Log tagging, field extraction, acknowledgment text |
| `D2` | Procedural work: multi-step tool use, follow a written runbook, fix a failure whose cause is already stated, write a test from a template | Standard deployment, routine brick operation |
| `D3` | Derivation: infer the action from principles, resolve conflicting evidence, plan across a whole universe, decide what proof is sufficient | Clean-sheet TEST, incident diagnosis, parent-side repair |
| `D4` | Architecture: change the law or the intent, design taxonomy, decide cross-universe promotion | Doctrine work — **human co-signature required** (Rule 24) |

`D4` is never dispatched autonomously, whatever the engine's capability.

## Axis 3 — Throughput (how fast, order of magnitude)

Orders of magnitude, not benchmarks. What matters is the class, not the number.

| Tier | Recommended | Interaction budget | Typical of |
| :--- | :--- | :--- | :--- |
| `T0` | ≳ 500 tok/s | Instant, sub-second | Voice acknowledgment, micro-tasks. Reserved — never a general chat engine (Rule 0H) |
| `T1` | ≳ 50 tok/s, first token < 1 s | Conversational | Cockpit chat, operator interaction |
| `T2` | ≳ 10 tok/s | Minutes acceptable | Background jobs, queued work |
| `T3` | Any | Hours acceptable | Batch, offline analysis, bulk ingestion |

## Axis 4 — Context horizon (how much history the work needs)

Depth and throughput describe the thinking. They say nothing about **how far back
the work has to see** — and that turns out to separate two agents far more than
their raw capability does.

| Horizon | The work needs | Typical of |
| :--- | :--- | :--- |
| `H0` | Nothing but its own input | Classification, extraction, acknowledgment |
| `H1` | The current session | A conversation, a deployment run |
| `H2` | The state of this universe | Diagnosis, repair, a decision about this system |
| `H3` | The operator's accumulated usage — months of prior exchanges | Advice about direction, recognising a pattern the operator has lived through |

This axis exists because of an asymmetry the operator meets daily, not because of
theory. The same human talks to a **conversational assistant** — which carries
`H3`, the long history of everyday use — and to a **task-scoped engineering
agent** — which lives at `H1`/`H2`, sharp on the present work and blind to
anything not in front of it. They are as different from each other as two vendors
are, sometimes more.

The friction is that **the human uses both the same way.** They do not switch
register when they switch surface, and they should not have to. So the
declaration belongs to the work, not to the person: a job that needs `H3` must be
sent somewhere that has `H3`, and a job that only needs `H0` must never be
charged for a horizon it will not use.

A brick that requires a horizon it cannot be given must say what it does about
it, exactly as with depth and throughput — `refuse`, `queue`, or run and record
the limitation. An answer given at `H1` to a question that needed `H3` is not
wrong in form; it is confident and under-informed, which is worse.

## Axis 5 — Degradation policy (what happens when you cannot have it)

You work with what is available. That is a fact, so it must be a **declared
decision**, not an accident:

| Policy | Meaning |
| :--- | :--- |
| `refuse` | The brick must not run below its declared requirement. Failing loudly is correct. |
| `queue` | Wait for a qualifying engine. The job is parked as `AWAITING_CAPACITY`, the human is told. |
| `allowed-with-note` | Run anyway, and record the degradation as an audit event so the result is never mistaken for a nominal one. |

A brick that runs degraded **silently** is a Rule 0G violation: the output looks
like nominal output and nothing in the record says otherwise.

---

## The declaration

In the brick's `INTENT.md`:

```markdown
## Cognition
- capacity-class: infra-ops
- depth: D2
- throughput: T2
- horizon: H2
- degraded: queue
- rationale: Deploys and supervises containers from a written contract; no
  ambiguity to resolve, no interactive latency requirement.
```

In `manifest.json`, per brick (optional, overrides the brick default for this
universe only — [Rule 33](../../RULES.md): specialize by declaration before forking):

```json
"bricks": {
  "brick-queue": {
    "source": "base",
    "perimeter": "P1",
    "package": "@shaper/pkg-queue",
    "image": "img-queue",
    "intent": "./bricks/brick-queue/INTENT.md",
    "role": "Async work ledger for this universe",
    "cognition": {
      "capacityClass": "infra-ops",
      "depth": "D2",
      "throughput": "T2",
      "horizon": "H2",
      "degraded": "queue"
    }
  }
}
```

---

## Measurement and economic policy

From the actual target host, enumerate reachable engines and run a bounded probe representative of the declared work, including actual tool use when required. Record correctness, reachability, observed latency/throughput, cost class, engine/harness configuration and measurement time. A bare echo cannot qualify a file-writing or multi-step role; public rankings are advisory.

Eliminate engines that fail the capability contract, then engines dominated on both cost and performance. On the remaining frontier apply the manifest's `enginePolicy`: `frugal` (default, cheapest; fastest among equal cost), `swift` (best measured performance), or `budget` (best performance below the operator's stated per-task ceiling). Do not invent an undisclosed cost/performance weighting. A timed-out candidate is unavailable for this measurement, not silently usable.

The horizon must actually be supplied through authorized context; declaring `H3` does not grant access to private histories or promise model memory. Unavailable requirements follow the declared degradation policy and remain visible.

## Concrete engines and versions

Generic requirements never pin a model as universal law. A specific adapter profile may name its selected provider and dependency versions; measured runtime matrices and dated proof record actual engine/model/harness versions. A source-controlled proof is descriptive, not authority to reuse a stale measurement. Re-measure the candidate deployment and preserve its result with the realization.

A router, if constructed, obeys this same contract and has its own intent, tests and real execution proof. Its presence is not assumed by a declarative field. See the [operating contract](../agent/OPERATING-CONTRACT.md) and [common bridge](../intents/cognition-bridge.md).
