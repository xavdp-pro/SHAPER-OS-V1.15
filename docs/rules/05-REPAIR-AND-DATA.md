# Rules 23–31 — Repair authority and data integrity

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
The original rule identifiers, scope and binding force are unchanged.

<a id="rule-23"></a>
### Rule 23: External Healing Law (Parent Repairs Child)
* **Zero Self-Destructive In-Flight Modification**:
  * An AI agent NEVER modifies its own active infrastructure files, its bridge server, or its running process during execution .
  * Any structural repair, recovery, or update on an Agent of Level $K$ is MANDATORILY performed by the Parent Supervisor Agent of Level $K+1$ (or by the human operator) operating out-of-band at cold boot.

---

<a id="rule-24"></a>
### Rule 24: Root Guardian Law (Sentinel / Human Repairs Root)
* **Out-of-Band Root Supervision**:
  * For the Root Universe of a fractal tree (Level $N$, with no parent in the tree), integrity monitoring and emergency patching are performed by a **Sentinel Sidecar Agent** or by the **Human Operator using an external IDE (Cursor, Antigravity, Claude Code)** via an isolated control channel.
* **The root universe is the master root's** : the tree has one top, held by the **master root** of Rule 37 — the founding tandem of a human Steward and the root agent under their direct control, root from underneath every host (Rule 36). Its own universes carry the governor and the makers, which take direction from it alone. It grants every jurisdiction. A **jurisdiction root** holds full power inside what it was granted, down to the pods of its universes, yet it is never the root universe of this rule: it sits under a parent, reaches no host, and is repaired from above like any child (Rule 23).

---

<a id="rule-25"></a>
### Rule 25: Canary Deployment & Downward Rollback (Anti-Propagation)
* **Progressive Fleet Updates**:
  * Whenever a Parent Universe distributes a configuration or brick update to its child fleet:
    1. **Canary (1/N)**: Deploy to 1 pilot child universe only.
    2. **Observation Period**: Monitor logs and health for $T$ minutes (bake time, default 5 min).
    3. **Phased Rollout**: If the canary passes its gate → deploy to 10%, then 100% of the fleet.
    4. **Automatic Rollback**: At the first failure on the canary, immediately roll back without touching the rest of the fleet.
* **The Canary Gate Is the Typed Gate (R20), Not the Health Port**:
  * A `200 OK` on `/api/health` is a liveness signal, never a validation signal. A canary is declared green only when it has produced at least one real deliverable of its universe's nominal type **and that deliverable passed its Rule 20 typed verification contract**.
  * Bake time without a produced-and-verified deliverable does not count as green: the rollout stops and escalates rather than proceeding blind.

---

<a id="rule-26"></a>
### Rule 26: Complete Database Isolation (MariaDB per Functional Podman)
* **Zero Domino Effect on Data**:
  * To guarantee total blast-radius isolation, each functional Podman operates
    its own MariaDB instance inside its own security, storage and lifecycle
    boundary. There is no shared database at universe level.
  * Asterisk, Helm, Vault, Logger, Queue and every other functional Podman each
    own a different MariaDB instance and credentials. A failure, migration or
    compromise of one database must not reach another function.
  * A functional Podman's birth and qualification fail when its MariaDB is
    absent, unhealthy, reachable outside its boundary, non-persistent, or lacks
    a successful restore proof. CSV, JSONL, SQLite or another Podman's database
    cannot substitute for this gate.
  * Qualification also fails unless the running function uses the Linux account
    named by its functional slug, its MariaDB account and database use that same
    slug, the password is read from
    `/apps/<functional-slug>/etc/mysql/localhost/passwd` with mode `0600`, and
    credentials belonging to another functional Podman are refused.
  * Database administration proof uses the local MariaDB root CLI path; application
    behavior proof uses only the confined functional account. Passing one path does
    not prove the other.
  * **Legacy transition**: an already-running instance that predates this
    invariant may continue unchanged while it remains serviceable; its existing
    SQLite, CSV or JSONL store is recorded as technical debt, not presented as
    compliance. No forced in-place migration is implied. The gate becomes
    mandatory when that functional Podman is rebuilt, replaced, rematerialised
    or promoted: the new artefact must carry its private MariaDB and pass the
    complete qualification above before it takes over.
  * The Central SaaS database holds exclusively the node inventory registry and global billing data.

---

<a id="rule-27"></a>
### Rule 27: Reconciliation Convergence Guard (Anti-Flapping & Resting Degraded State)
* **A Reconciliation Loop That Cannot Give Up Is a Storm Generator**: The owning reconciliation engine, which may be triggered by Maestro (desired manifest ↔ observed state persisted in its private database) MUST bound its own corrective action.
  * **Exponential Backoff**: Repair attempts on the same drift signature back off (e.g. 30s → 1m → 2m → 4m), never retry at fixed beat cadence.
  * **Bounded Attempts**: The realization declares a finite `maxHealingAttempts`; when none is supplied, the default is 5. After that configured number of attempts on the same drift signature, the supervisor STOPS attempting repair.
  * **Resting `DEGRADED` State**: The child universe is marked `DEGRADED` in the parent registry, its drift signature and last diagnostic are recorded, and the human operator is alerted. `DEGRADED` is a resting state, not a retry state — it never self-clears. Its authorized exits are specified below; `REAPED` is the terminal lifecycle state.
  * **How a `DEGRADED` row is left** : a DEGRADED row leaves that state by its account's explicit new ask, for the environments a robot may end (`dev`, `test`, `demo`) — the broken row's deadline becomes now, a maker reaps whatever half-exists and reports `REAPED`, and a fresh row is born beside it; the broken one was a failure the account was stuck behind, not a life to protect. A **`prod`** row leaves it only by human or Root Guardian action: a robot's re-ask is refused as a typed fact carrying the row id, no twin is born, and the reap recipe refuses to end a production universe (exit 4, reported `REAP_REFUSED` — a fact, not a failure) so that the row rests and the alarm leaves out of band. The same bounds apply to the governor's own offers: a reap that failed is offered again under exponential backoff and never beyond `maxHealingAttempts`; a reap that was refused is never offered again.
  * **Fleet-Wide Circuit Breaker**: If more than 20% of a fleet enters `DEGRADED` within one bake window, the parent suspends ALL reconciliation and rollout activity on that fleet and escalates. A systemic fault must never be amplified N times.
* **The Escalation Channel Is Declared, Never Assumed**: "Alert the operator" is meaningless until the channel exists. Each universe declares its `alerting` channel in `manifest.json` — mobile push, mail, Telegram, or an existing prod-alerting relay. The channel depends on what is being watched and is decided case by case; the doctrine imposes only the contract:
  * It reaches a **human out-of-band** — never a UI nobody is looking at.
  * It is **tested at deploy time** like any other brick: an unverified alert path is an absent alert path (Rule 0G).
  * A universe with no declared channel MUST NOT be promoted beyond DEV.
* **Rationale**: Without these bounds, one invalid manifest on a 50-child fleet produces 50 simultaneous restart loops — the reconciliation engine becomes the outage.

---

<a id="rule-28"></a>
### Rule 28: Sovereign WAF Rule Validation (No Unproven Guardian)
* **An AI-Generated Allow-List Is a Hypothesis, Not a Defence**: The sovereign WAF/aiguilleur allow-list is synthesized by the parent agent that knows the application's legitimate routes. It is therefore an artefact like any other and falls under Rule 20.
  * **Mandatory Attack Corpus**: Before any WAF ruleset reaches production, it MUST pass a versioned attack corpus stored in the repository — at minimum: SQLi, XSS, path traversal (`../`), verb violation on a `GET`-only route, and rate-limit saturation.
  * **Mandatory Legitimate Corpus**: The same ruleset MUST let through a versioned corpus of legitimate business requests. A WAF that blocks real customers is an outage, not a protection.
  * **No Silent Rule Drift**: Any regeneration of the allow-list re-runs both corpora and is deployed to the fleet under Rule 25 (canary first).
* **Scope Discipline**: The sovereign layer's uncontested role is **routing** (routing universe → container) and **precomputed cache serving**. Generic attack signature filtering SHOULD delegate to a maintained engine (OWASP CRS via Coraza / ModSecurity) rather than being reimplemented; the doctrine forbids presenting a hand-rolled signature filter as equivalent protection.

---

<a id="rule-29"></a>
### Rule 29: Constructive Integrity (Every Fixed Bug Becomes a Test)
* **The System Grows a Memory of Its Own Failures**: Any resolved defect — in code, in a manifest, in a WAF rule, in an agent prompt — MANDATORILY gives birth to a new non-regression test committed alongside the fix.
* **No Fix Without Proof**: A patch whose accompanying test would still pass on the unpatched code does not demonstrate anything and is rejected.
* **A Correction Lives Where It Survives**: A defect met while deploying or operating a universe is corrected in the **generic path** — the brick, the package, the template, the example deploy script — never only in the universe where it appeared. Its test is placed where it will still run after that universe is gone.
  * **Why this is a rule and not advice**: a `-test` universe is destroyed by Rule 10, and a `-dev` one is disposable by design. A fix written into an instance is deleted with the instance, and the next clean sheet meets the same wall having learnt nothing. The next clean construction must inherit the correction from its owning source and test.
  * **The test decides where the fix belongs**: if the non-regression test would disappear with a universe, the fix is in the wrong place. Move both.
  * **A universe may still specialise**: this forbids *correcting* in an instance, not *parameterising* one. When a defect is genuinely specific to one deployment, say so in that universe's INTENT and explain why the generic path is right as it stands.
* **Antifragility Contract**: This is what makes the fractal tree antifragile rather than merely resilient — each incident permanently raises the floor for every universe instantiated afterwards. That floor only rises where the correction outlives the universe that found it.

---

<a id="rule-30"></a>
### Rule 30: Snapshot Before Migration (Data-Bearing Changes Are Not Canary-able)
* **Why This Rule Is Separate from Rule 25**: The canary protects against a bad configuration, because a configuration can be rolled back. A database migration **carries data**: rolling back the code does not bring back a dropped column. Progressive rollout is necessary here but not sufficient.
* **The Non-Negotiable Sequence**:
  1. **Full snapshot first** — the owning functional Podman's MariaDB dump plus its persistent volumes, taken immediately before the change, never a nightly backup "close enough".
  2. **Verified restore** — the snapshot is restored into an ephemeral sandbox and proven loadable. An unverified backup is not a backup (Rule 0G).
  3. **Only then** apply the migration, canary first per Rule 25.
  4. **Rollback = restore the snapshot**, not "run the reverse script".
* **Preferred Refinement (Expand / Contract)**: where feasible, make the change non-destructive in stages — add the new column, write to both, migrate readers, and only drop the old column in a later release once every universe in the fleet is confirmed migrated. Destructive and reversible steps never travel in the same deployment.
* **Fleet Scope**: a schema change affecting N functional Podmans is N independent migrations, each with its own snapshot. One shared migration transaction across functions or the fleet is forbidden — it would recreate the common point of failure Rule 26 exists to remove.

---

<a id="rule-31"></a>
### Rule 31: Declared Data Lifecycle (Per Universe, Not a Universal Policy)
* **The Doctrine Forces the Declaration, Not the Policy**: retention and erasure requirements depend entirely on the client and the use case. A personal mailbox and a client business database can need different policies; each declares the policy appropriate to its data and mandate. Imposing a single global policy would be wrong in both directions.
* **Every Universe Declares Its `dataLifecycle` in `manifest.json`**, with at minimum:
  * `personalData`: `true` / `false` — does this universe hold data about identifiable people?
  * `retention`: duration or `unlimited`, per data class (GED documents, JSONL logs, vector collections, database rows).
  * `onTermination`: what is destroyed, what is exported to the client, and in what format, when the universe is decommissioned.
* **`personalData: false` Is a Valid and Common Answer** — but it must be written down, not left silent. Silence is not a declaration.
* **Erasure Is Fractal**: deleting a client's data means deleting it in every store of that universe — MariaDB rows, `sav/` volumes, GED files, **and its Qdrant collection**. A vector left behind is a leak; the isolation of Rule 22 is what makes this deletion tractable in the first place.

---


## Reading continuation

[Previous part](04-SERVICES-AND-QUALITY.md) · [Next part](06-FRACTAL-CONSTRUCTION.md)
