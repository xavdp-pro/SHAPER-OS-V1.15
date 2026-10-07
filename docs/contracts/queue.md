# Queue Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Queue is a generic asynchronous job service with progress and SSE, not a business agent or a source of authority. It owns a private MariaDB and retains its own job evidence.

## Lifecycle and crash semantics

The normal execution path is `PENDING → RUNNING → COMPLETED | FAILED`. The consumer explicitly advances state, or an enabled `agent.inject` worker does so. Commit each transition durably before exposing it.

[Rule 20](../../RULES.md#rule-20) additionally requires `NEEDS_CONTRACT`: a durable, non-success hold when the output type has no declared verification contract. Preserve the result and evidence, release the execution lane and escalate to the human, who declares the reusable contract for that type. This hold is neither an executing `RUNNING` job nor a terminal `COMPLETED` or `FAILED` outcome; it survives restart without execution-timeout failure or automatic replay. Once the contract is declared, resume verification of the retained result, not automatic re-execution of the producing action. Reconcile uncertain external effects before any further execution. Contract declaration alone is not success: the typed verification contract must pass before `COMPLETED`.

Durability preserves the record, not an in-flight computation. After restart, persisted `PENDING` jobs may receive their first execution. A formerly `RUNNING` job is adopted as `FAILED` with an interrupted/unknown-outcome reason and is never automatically replayed. The owning unit must inspect its action ledger and external effects, reconcile uncertainty, then re-enqueue idempotently when appropriate. A failed or missing conversation turn cannot prove no effect happened.

A lane cannot remain held by silence. For an executing job, bound terminal-event waiting with `QUEUE_RUN_MAX_SECONDS` (default 900); on expiry fail with the explicit reason that the watcher timed out and the actual outcome is unknown, and free the lane. This is not proof the action failed to take effect.

## Evidence and transport

Queue itself records and emits `JOB_CREATED` and, on the corresponding terminal transition, `JOB_COMPLETED` or `JOB_FAILED`, correlated by job ID, including jobs enqueued directly. A `NEEDS_CONTRACT` hold remains observable with its reason and human escalation; it emits neither terminal outcome. Preserve pending audit delivery durably in its own transaction/outbox and retry it; a down Logger is observable and must not erase evidence or fabricate success. SSE and event hooks accelerate observation, while stored records remain authoritative.

`type` and `payload` are opaque to the generic queue core. Its optional worker recognizes only `type=agent.inject`, forwards the declared request to the selected bridge and records its terminal result. When final text exists it is stored as `job.result.answer`, with exit/result status; a bridge terminal event does not by itself satisfy the typed verification gate or resolve a `NEEDS_CONTRACT` hold.

| Field | Requirement and meaning |
| :--- | :--- |
| `type` | `agent.inject` for the optional dispatch worker |
| `payload.message` | Required precise instruction |
| `payload.conversation` | Optional bridge session/workspace identifier, resolved by the adapter |
| `payload.bridgeUrl` | Optional declared bridge address, otherwise the realization's `QUEUE_BRIDGE_URL`; no invented host |
| `payload.model` | Optional engine selected by the measured cognition policy |
| `payload.context` | Context snapshot/extra task context supplied at creation |
| `totalSteps` | Optional progress denominator, default 1 |

Before dispatch, resolve the current authorized role, jurisdiction, resources and per-action/type policy; the queue grants no broader rights. On execution, reload current context and deltas plus the owning unit's action evidence according to the [bridge contract](../intents/cognition-bridge.md). A queued snapshot neither freezes authorization forever nor replaces that evidence.

The constructor declares the precise enqueue/read/SSE schemas, hold notification and verification-resumption semantics in the realization and proves real restart, orphan reconciliation, terminal timeout, `NEEDS_CONTRACT` persistence and resumption without duplicated effects, independent downstream effects and audit delivery. [Rule 20](../../RULES.md#rule-20) prevents `COMPLETED` before the typed acceptance contract succeeds.
