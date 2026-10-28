# Functional Podman and private MariaDB construction profile

Profile lineage identifier: **SEP22-CONTAINER-MARIADB**.
Current scope follows the [25 October direction](../../decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md).
The filename and lineage identify the established foundation; adopted revisions
remain explicit. Owners: [Rules 4/11/26](../../RULES.md), [composition](../architecture/COMPOSITION.md),
[topology](../architecture/TOPOLOGY.md) and the detailed [unit contracts](../GOVERNING-CORPUS.md).

## Applicability

The current construction model uses Podman functional boundaries and complete
private MariaDB application persistence. Every new or replaced functional owner
carries that contract. An agent selects ordinary implementation details inside
this foundation; changing the foundation requires an explicit new direction.
The [24 September decision](../../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md)
and [Turbinobash method](../../decisions/2026-10-10-UNIT-DATABASE-TURBINOBASH-METHOD.md)
provide its lineage. The 25 October direction changes hosting-profile selection
and table-partition applicability, preserving functional ownership.

## Practical topology

Infrastructure hosts the selected profile: direct functional Podman containers,
LXC with functional containers, or nested Podman with functional containers.
The class declares the profile and required host capabilities; its instance
records actual placement. A universe (space) organizes cell membership and
relationships. Legacy `univ-*`
profiles retain their operational-composition usage with an explicit class-role
mapping, independently of physical hosting.

For Linux, macOS or Windows development, declare the compatible Linux runtime
backend and environment-specific mounts, networking, storage and private config.
The same class, interfaces and state owners continue into production through
versioned builds, locked artifacts or coherent restoration. [Rule 11](../../RULES.md#rule-11)
owns containment; no logical nesting requires automatic physical nesting.

## Preserved choices

Each functional unit (component) has one responsibility, one Podman runtime boundary,
one system identity and its own MariaDB server in the same container. The
functional slug names the application account, database account and database.
The server uses a separate engine account and private local Unix socket;
application access and administrative root access remain distinct. Application
accounts receive neither administrative credentials nor schema-management rights.
[Rule 4](../rules/02-CONSTRUCTION.md#rule-4) owns the complete filesystem,
credential, identity and administration contract.

All authoritative application state belongs to that owner's MariaDB: business
records, schedules, occurrences, queue leases, logs, agent session/context
continuity, action evidence and pending effects. Native engine stores are
managed working material or reconstructible projections. Durable media and
other artifacts retain database-owned identity, lifecycle and recovery links.
A selected derived vector index is reconstructible and does not replace MariaDB.

Partition tables according to their workload, volume, queries and retention.
Ordinary tables remain appropriate where partitioning adds no useful benefit.
UTC monthly histories are a supported declared policy; the
[earlier monthly direction](../../decisions/2026-10-13-MONTHLY-SQL-PARTITIONS.md)
retains its historical scope. Rules 4 and 26 now apply the explicit 25 October
workload-based policy. Rollover alone grants no deletion authority.

The generic stem-cell base contains Vault, Logger, Queue and Maestro. Vault,
Logger and generic Queue are P1; deterministic Maestro is P2. The reference
adds OpenCode as its default cognition bridge under the
[24 September choice](../../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md).
The base remains operational without cognition; Maestro is idle without schedules.
A specialized cell (service) adds one or more domain functional units and their owning
contracts. Its class and specialization versions remain distinct from the
identity, credentials, state and placement of each instance.

Each owner preserves pending evidence with its local state transition. Logger's
receipt, Queue's responsibility and the consumer's effect retain different
meanings. Cross-owner commands/events carry stable identities and reconciliation;
a local transaction is not a distributed transaction across databases.

## Scope placement

A universe declares its cell memberships, scoped governance and permitted
crossings. It does not automatically acquire a duplicate base stack merely by
existing. Functions actually owned at universe level are declared as such with their
own state and lifecycle. Aggregation is a separate receiving function, not an
implicit merger of source databases or histories.

The realization records logical parent/child relationships, finite resource and
creation bounds, actual authority on both sides of each crossing, and the owner
of recovery/retirement. A standing mandate covers matching work without renewed
approval. Containment, hosting and a screen request grant no authority by themselves.

| Record | Meaning |
| --- | --- |
| Composition | Stable class, specialization and instance identities; base and domain functional units; universes |
| Placement | Selected profile, host capabilities and physical boundaries |
| Doors | Sender/receiver, purpose, data/actions, standing authority, refusal and evidence |
| Fractal scope | Governor responsibilities, maker/worker jurisdiction, finite creation bounds and external recovery owner |
| Source custody | Product intentions/code and separate private project `-lab`; private user configuration/data |

## Bootstrap and recovery direction

The authorized parent supplies initial Vault identity and separately held keys.
Vault verifies continuity before delivering scoped credentials. The actual
acyclic hard-dependency graph orders private state, Vault, Logger, Queue,
Maestro and the selected bridge; parallel work follows declared independence.
A readiness receipt carries its precise meaning rather than replacing a
consumer's acceptance or an independently observed effect.

Small owned state units support predictable maintenance and localized restore.
The cell declares PCA/PRA, RPO/RTO, consistent database/artifact capture,
separate backups and replicas, and externally controlled writer activation.
Restoration uses known class/schema/artifact revisions, excludes stale writers,
and reconciles uncertain effects before work resumes. [Rules 12/16/30](../../RULES.md)
own protection and migration. An image rebuild preserves its non-reproducible
state and cryptographic identity.

Read [Vault](../contracts/vault.md), [Logger](../contracts/logger.md),
[Queue](../contracts/queue.md), [Maestro](../contracts/maestro.md),
[bridge](../intents/cognition-bridge.md) and [lifecycle](../agent/LIFECYCLE.md)
for their exact interfaces, authority and recovery obligations.
