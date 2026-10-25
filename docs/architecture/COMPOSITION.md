# Composition across scales

Stable concept IDs: [human-ai-tandem](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#human-ai-tandem),
[component](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#component),
[stem-cell](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#stem-cell),
[service](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#service),
[space](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#space),
[class](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#class),
[specialization](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#specialization),
[instance](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md#instance).

Concept route: [ecosystem composition owner](https://github.com/xavdp-pro/shaper-ecosystem)
→ [independent glossary](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md)
→ this SHAPER OS projection → [owning laws](../../RULES.md).
Adoption: [25 October direction](../../decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md).

## Composition contract

| Scale | Responsibility | Owning relationship |
| --- | --- | --- |
| Infrastructure | Host execution, connectivity and recovery capacity | Hosts a selected realization; placement grants no business authority |
| Component / functional unit | One bounded responsibility, interface, identity and private state | Provides a capability; implementation packages and images realize it |
| Generic stem cell | Reusable base composition | Pins compatible base components and their contracts |
| Specialized cell / service | Base plus one or more domain components | Specializes the base; exposes a declared business/service contract |
| Logical space | Organizes service instances and permitted relationships | Membership and presentation, independently of host/container boundaries |
| Fractal scope | Repeats bounded governance at an appropriate scale | Governor(s) own scoped desired state; makers/workers carry out authorized work |
| Human–AI tandem | Steers purpose, judgment and delegation at every scope | Grants and revises mandates; retains the means to understand and redirect |

The current shared glossary uses **logical space / universe** for a stable
organizational scope relating services. Earlier V1.15 `univ-*` classes and
protocols also use “universe” for a bounded operational composition. Their
recorded class role maps explicitly to the current concept; identifiers and
instances remain unchanged. A legacy service composition is not silently
reclassified or renamed, and neither usage requires a physical outer container.

OS specifies intentions and laws. Runtime enforces permissions and performs
stateful effects. Workspace presents and requests permitted work. These three
responsibilities cross the composition scales; they are not three container
levels. P1/P2/P3 remain functional [perimeters](PERIMETERS.md), another axis.

## Class, specialization and instance

A class is a versioned reusable definition. A specialization derives a declared
domain composition or behavior from a base class, preserving its inherited
invariants and recording intentional deltas. An instance has a stable identity,
selected class/specialization versions, owner, environment, placement and state.
Updating a class definition does not silently mutate existing instances.
A repository can own a class or related definitions; repository count and slug
are not runtime cardinality. The [governor protocol](../contracts/governor.md)
retains its scoped account/class uniqueness and immutable live-row parameters.

A telephony service and a CRM service specialize the base independently. A
softphone requests authorized telephony actions; a CRM owns customer records.
Their integration uses declared commands/events and stable references, never
cross-database access. A shop manager owns its order/provisioning contract;
approved work reaches a governor/maker and then workspace membership through
explicit owners. A screen, payment signal or membership link supplies no
additional infrastructure authority. Domain intentions remain with their owners.

## Persistence and continuity

Every functional owner has its private MariaDB inside its functional Podman
boundary under [Rules 4 and 26](../../RULES.md). Business records, scheduler
registrations, leases, logs, action histories, durable CLI sessions, context
revisions and engine-session mappings have explicit authoritative owners there.
Native engine files are managed working material or recoverable projections;
they do not become a second authoritative application store. Media and other
nonrelational payloads use declared durable artifacts with database-owned identity
and lifecycle. A derived search/vector index is optional and reconstructible.

Partition tables when workload, size, query and retention needs justify it.
Declare ordinary tables where partitioning supplies no useful benefit. UTC month
partitions are a selected policy, not a rule for every history. Administrative
DDL, retention and restore remain separate governed operations.

Small elementary state units contain local failures. [Rule 16](../../RULES.md#rule-16)
connects consistent captures, replicas, service redundancy, independent recovery
means and controlled writer activation. Declare BCP/DRP (PCA/PRA), RPO/RTO and
recovery dependencies for the service; no component count creates a guarantee.

## Local development and production

Declare Linux, macOS or Windows host capabilities and the compatible Linux
runtime backend used for functional Podman containers. Direct hosting, LXC and
nested hosting are selected profiles under [Rule 11](../../RULES.md#rule-11).
Local and production instances use the same class contracts with explicit private
environment configuration, credentials and data boundaries. Select a source build,
a locked artifact or a coherent restore deliberately; preserve class, schema,
artifact and recovery-point identity across that choice.

## Navigation back to the owners

[Source roles](SOURCE-ROLES.md) explains custody and lookup. [Topology](TOPOLOGY.md)
separates dependency from containment, authority, ownership and placement.
[Profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md) binds the selected construction
choices. [Lifecycle](../agent/LIFECYCLE.md) owns promotion; [LAW](../../LAW.md)
owns adoption. These projections link outward rather than redefining domain laws.

## Referrers in this edition

- [AGENTS.md](../../AGENTS.md): applies this composition projection.
- [INTENT.md](../../INTENT.md): applies this composition projection.
- [LAW.md](../../LAW.md): applies this composition projection.
- [README.md](../../README.md): applies this composition projection.
- [RULES.md](../../RULES.md): applies this composition projection.
- [decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md](../../decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md): applies this composition projection.
- [docs/CONTEXT-INDEX.md](../CONTEXT-INDEX.md): applies this composition projection.
- [docs/GLOSSARY.md](../GLOSSARY.md): applies this composition projection.
- [docs/GOVERNING-CORPUS.md](../GOVERNING-CORPUS.md): applies this composition projection.
- [docs/IDEAL-SCENE.md](../IDEAL-SCENE.md): applies this composition projection.
- [docs/architecture/LEXICON.md](LEXICON.md): applies this composition projection.
- [docs/architecture/NAMING.md](NAMING.md): applies this composition projection.
- [docs/architecture/SOURCE-ROLES.md](SOURCE-ROLES.md): applies this composition projection.
- [docs/architecture/TOPOLOGY.md](TOPOLOGY.md): applies this composition projection.
- [docs/architecture/VOCABULARY-BOUNDARY.md](VOCABULARY-BOUNDARY.md): applies this composition projection.
- [docs/learning/02-LAYERS-AND-SCOPES.md](../learning/02-LAYERS-AND-SCOPES.md): applies this composition projection.
- [docs/profiles/SEPTEMBER-CONTAINER-MARIADB.md](../profiles/SEPTEMBER-CONTAINER-MARIADB.md): applies this composition projection.
- [docs/rules/07-TREE-AND-FLEET.md](../rules/07-TREE-AND-FLEET.md): applies this composition projection.
