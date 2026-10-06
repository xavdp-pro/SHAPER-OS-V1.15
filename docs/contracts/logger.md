# Logger Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Logger supplies append-only structured audit for telemetry, execution and security evidence. Each event carries `timestamp`, `pod`, `level`, `event`, `data` and `duration_ms`.

* The functional Logger owns its private MariaDB. Audit records are append-only: no silent mutation or truncation. A JSONL stream/export uses one event per line and may be written under the declared `<LOG_DIR>/<POD>/activity.jsonl`; it does not replace required durable records.
* Provide in-process collection or a declared HTTP gateway as needed, keeping the reusable core free of unnecessary dependencies. Runtime language/library choices belong in the realization.
* Persist before acknowledging/streaming an event; distinguish accepted durable evidence from a merely open connection. Declared retention and erasure requirements still apply to data payloads and backup copies.

<a id="identity"></a>
## Service identity

Every service announces `service: "brick-<component>"` on `/api/health` and `/api/vitals`. The supervisor relies on that identity. A fixed version suffix cannot substitute for the component's identity; update the whole contract consistently.

<a id="sibling-paths"></a>
## Import placement

A built image must place reusable packages at the paths their real importers resolve. Test the actual import inside the image, not whether its build file mentions a dependency. Keep source/import names and destination paths consistent.

<a id="evidence"></a>
## Persisted evidence versus stream

`GET /api/events` is a live SSE stream. Opening it proves only connection; use a bounded stream observation. `GET /api/events/last` returns retained events and supports evidence checks. Correlate expected job/run/action identifiers and inspect actual payloads. A check that cannot fail for absent evidence is not an evidence check.

See [Queue](queue.md), [Proof](../agent/PROOF.md) and [Rules 4, 20 and 26](../../RULES.md).
