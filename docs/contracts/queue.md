# Queue Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Queue is a generic asynchronous job service with progress and SSE, not a business agent or a source of authority. It owns a private MariaDB and retains its own job evidence.

## Lifecycle and crash semantics

The states are `PENDING → RUNNING → COMPLETED | FAILED`. The consumer explicitly advances state, or an enabled `agent.inject` worker does so. Commit each transition durably before exposing it.

Durability preserves the record, not an in-flight computation. After restart, persisted `PENDING` jobs may receive their first execution. A formerly `RUNNING` job is adopted as `FAILED` with an interrupted/unknown-outcome reason and is never automatically replayed. The owning unit must inspect its action ledger and external effects, reconcile uncertainty, then re-enqueue idempotently when appropriate. A failed or missing conversation turn cannot prove no effect happened.

A lane cannot remain held by silence. Bound terminal-event waiting with `QUEUE_RUN_MAX_SECONDS` (default 900); on expiry fail with the explicit reason that the watcher timed out and the actual outcome is unknown, and free the lane. This is not proof the action failed to take effect.

## Evidence and transport

Queue itself records and emits `JOB_CREATED` and `JOB_COMPLETED` or `JOB_FAILED`, correlated by job ID, including jobs enqueued directly. Preserve pending audit delivery durably in its own transaction/outbox and retry it; a down Logger is observable and must not erase evidence or fabricate success. SSE and event hooks accelerate observation, while stored records remain authoritative.

`type` and `payload` are opaque to the generic queue core. Its optional worker recognizes only `type=agent.inject`, forwards the declared request to the selected bridge and records its terminal result. When final text exists it is stored as `job.result.answer`, with exit/result status; the terminal event drives success or failure.

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

The constructor declares the precise enqueue/read/SSE schemas in the realization and proves real restart, orphan reconciliation, terminal timeout, independent downstream effects and audit delivery. [Rule 20](../../RULES.md) prevents `COMPLETED` before the typed acceptance contract succeeds.
