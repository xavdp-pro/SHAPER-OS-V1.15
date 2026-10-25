# Provider-neutral Bridge Status Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Source role: SHAPER OS owns the provider-neutral `shaper-bridge/v1` status,
readiness and capability protocol in this page. The ecosystem's
[`component:cognition-bridge`](https://github.com/xavdp-pro/shaper-ecosystem/blob/main/chapters/components/cognition-bridge.md)
owns the generic mental intention; this edition's [continuity intent](../intents/cognition-bridge.md)
projects its governing obligations. Adapter realizations own exact payloads and
provider transport mappings at their selected versions, preserving this protocol
identity without redefining its status meaning.

1. `GET /api/status` returns protocol identifier `shaper-bridge/v1` with declared readiness and capabilities.
2. Callers branch on capabilities, never provider names. The common contract names no engine, model, CLI or external provider.
3. `ready: true` means the adapter can accept work; it proves neither successful model execution nor permission for an action.
4. Every run is correlated to its Runtime evidence and terminal result.
5. Before promotion as the universe's active core bridge, a realization proves this protocol and the required capabilities.

The [common cognition-bridge intent](../intents/cognition-bridge.md) defines the human mandate, session creation/resumption, context refresh, durable action evidence and DEV/PROD execution semantics. [Rule 8](../../RULES.md) retains the agent HTTP surfaces. The constructor declares precise payload schemas and provider transport mappings in the realization, preserving these meanings; this short status contract does not invent a session route absent from the provider-neutral protocol.
