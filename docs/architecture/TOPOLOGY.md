# Declarative Dependency Topology

## Composition and source graph

[Composition](COMPOSITION.md) owns the scale model; [source roles](SOURCE-ROLES.md)
owns canonical documents and reverse navigation. Link every functional unit (component)
or cell (service) node to its class/specialization definition, stable instance identity where
applicable, owning intent and source revision. Distinguish `contains`, `requires`,
`governs`, `owns-state`, `hosted-on`, `realizes` and `derived-from` relationships.
Only hard startup `requires` must be acyclic; governed event feedback can be
cyclic without becoming a startup cycle. Every edge names its purpose and owner,
and indexes its referrers. `optionalBrick` and existing `bricks` fields remain
compatibility identifiers for functional units; this vocabulary change does not
silently migrate existing manifests.


> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

The constructor creates the realization's root `topology.json`: the single master dependency graph. A local `deps.json` may declare a scoped override without replacing that master. The OS documentation supplies the contract, not a prebuilt graph for every cell.

## Invariants

* Declare which units/packages depend on each other, their startup order, capabilities and host-volume mounts once. No hardcoded cross-unit URLs or hidden boot chains in scripts, service units or imports.
* The hard `requires` graph is directed and acyclic. `bootLayers` are parallel-safe waves; a dependent wave starts only when its required preceding nodes are actually healthy.
* Each actual package import appears in `packageImports` or the node's `requires`. Reusable packages declare logical dependencies and never know which cell or universe consumes them; cell overrides are declared, not silent mutations of the generic topology.
* Resolve abstract mounts, ports and service-manager ordering parameters at deployment. Human-stated constraints are recorded; otherwise the constructor makes ordinary choices within each intent. JSON does not duplicate philosophical prose or become an invented business rulebook.
* Validate graph structure, import alignment, resolved configuration and real health/ordering in the realization. Generate the validator when absent; no particular executable is supplied by this repository.

| Field | Meaning |
| :--- | :--- |
| `id`, `type` | Node identity and kind |
| `requires` | Hard dependencies, healthy before startup |
| `optional` | Soft dependencies; absence is declared and nonblocking for unrelated functions |
| `provides` | Capability tags used by composition |
| `port`, `bootAfter` | Declared listening and ordering requirements |
| `optionalBrick` | A functional unit available only when the chosen composition requires it |

P1/P2 are [perimeters](PERIMETERS.md), not boot group names. The selected reference boot path is Vault and required unit state → Logger → Queue → selected bridge/orchestration → Helm and extensions according to their actual dependencies. Parallel startup is allowed only where this graph proves independence.
