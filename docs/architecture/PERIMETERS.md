# The Three Perimeters

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

[Rule 0A](../../RULES.md) binds this taxonomy. Every component is classified into exactly one perimeter before construction or deployment. **P1/P2/P3 denote architecture layers, never machine names or ownership.** A client-specific authentication brick can still be P1.

| Perimeter | Objective | Functions |
| :--- | :--- | :--- |
| P1 — minimal socle | Generic infrastructure, zero business logic and zero mandatory LLM | Vault, Logger, authentication, generic Queue, boot and each unit's private database |
| P2 — agentic | Scheduling, cognition and the human–agent organism | Maestro, bridges, agent runtime, Helm, generic mail intake, GED/RAG for the organism |
| P3 — business | Persistent vertical products and business behavior | ERP, CRM, trade document handlers, client portals, business human-to-human chat |

## Separation obligations

1. P1 knows no P3 business rules, schemas, clients or prompts. P2 enriches the organism; it does not absorb business applications.
2. Helm is the same conversational interface for every authorized pilot. Its `/console`, including voice, is P2. A client owner does not make it P3. Business chat is a separate tenant/dossier-scoped real-time service, not Helm under a different name.
3. Construct P3 units in the universe class realization, not in the generic base or inside Helm. They have their own intent, code/image, port, UX/branding, authentication boundary, lifecycle and universe-owned volume. Reusable source packages are optional; a deployable brick must really build.
4. Every brick manifest states `perimeter`, `source` and, only for a fork, `forkedFrom`. Never infer these from a path, pilot identity or repository name.
5. A `ctx-*` or `task-*` carrying business behavior is P3 behavior even when hosted by P1/P2 units. It does not need a separate perimeter slot; the hosting universe's declared brick layers remain unchanged.
6. In the selected reference, establish Vault and required state before Logger, Queue and P2 dependents. The actual [topology](TOPOLOGY.md) determines healthy boot waves; a convenient group name such as `minimalSocle` never reclassifies a P2 node as P1.

## Classify by what the component does

A generic MIME parser can be P2; mailbox triage policy is P3. Generic template interpolation can be P2; invoice business fields are P3. A shared cognition transport belongs in the bridge layer; vertical structured-output behavior belongs with its product. Split responsibilities when necessary instead of pulling business logic down into P1.

Generic mail intake, semantic memory and a graphical console are optional extensions unless the selected composition needs them. An inventory of illustrative functions is not a claim that their implementation ships in this OS. Generate and qualify the chosen units following the [construction procedure](../procedures/01-REFERENCE-UNIVERSE.md).
