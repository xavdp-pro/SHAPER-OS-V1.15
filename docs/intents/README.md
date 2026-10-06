# Realization intents — ready-to-implement contracts

A realization intent states what an external implementation must provide so it
can be built, qualified and replaced against a stable meaning. The construction
agent can generate that implementation in a new separate workspace. SHAPER OS
contains intentions, obligations and verification questions; executable material
stays outside it. See the [repository boundary](../../INTENT.md).

## Read the shared contract before the adapter

| Intent | Role and authority |
| :--- | :--- |
| [Generic cognition bridge](cognition-bridge.md) | Shared mission, human-bounded jurisdiction, prepared context, session continuity, precise actions and independently checked evidence. |
| [OpenCode cognition bridge](cognition-bridge-opencode.md) | Scoped adapter selected by default for the reference universe; native session and tool integration qualified against the shared contract. |
| [Meta Muse cognition bridge](cognition-bridge-meta-muse.md) | Optional scoped adapter; distinguish API history replay from a CLI/tool realization. |

Other providers implement the same shared intent through their own declared
capabilities. Similar HTTP routes or a shared protocol name do not establish
identical context, tool, persistence or recovery semantics. Record source-observed
capabilities and missing obligations separately from executed qualification.

The [6 October direction](../../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md)
owns the common continuity requirement. Provider commands, exact wire schemas,
ports and model settings belong to the adapter realization; they never redefine
the generic contract. Historical implementations remain comparison or reuse
material, not code imported into this repository.
