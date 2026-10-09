# Maestro Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Maestro belongs to **P2**, the agentic perimeter, and is a deterministic scheduler: register tasks, pulse at declared cadence and spend no LLM tokens while idle. The handler decides whether cognition is needed; scheduling carries no business reasoning. Its membership in the four foundational units and its ability to run without an LLM do not make it P1.

* A task declares `slug` and `cadence`. A deployment may also declare label, port and routing fields. Vault keys and context paths are opaque references, not secrets embedded in the scheduler.
* Record every beat and its outcome in structured audit, correlated with any job it creates. Maestro's registrations, beat state and action evidence belong in its own private MariaDB.
* Before enqueueing, read the configured context and include its text in `payload.context`. An unreadable or empty declared context skips the beat with the exact reason. This records what was actually supplied without relying on later mounts or file content.
* `instruction` is the explicit request; `beatMessage` is the compatibility fallback for a registration that lacks it. Resolve that choice visibly in the concrete contract.
* A scheduled task remains within the human mandate and current per-action/type policy. A cadence cannot widen permissions. The executing unit reloads current context/deltas and prior effects before action, even when the creation snapshot exists.
* Keep runtime state local to its owning unit, call Queue/bridge through declared interfaces, and prove the real beat → job → effect → evidence loop. Scheduling does not authorize sending email or any other external act absent the task's mandate.

## Interactive work

Under [Rule 21](../../RULES.md#rule-21), Maestro records interactive work as
`AWAITING_HUMAN` in its own durable dispatch state and notifies the operator.
Retain the operation, input/context revision, reason and any correlated Queue job.
The realization declares that handoff explicitly: parked work occupies no
execution lane and is not an automatically runnable job after restart.
An operator taking up the work initiates the interactive path under current
authority; a beat or available slot never makes the class auto-dispatchable.
Record cancellation, expiry and completion, and reconcile prior effects before
any retry. Follow [Queue's generic parking and claim contract](queue.md#deferred-prerequisites-and-consumer-claims).

See [Queue](queue.md), [common bridge](../intents/cognition-bridge.md) and [naming](../architecture/NAMING.md).
