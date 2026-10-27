# 2. Layers, cells, universes and fractal relationships

Purpose: explain layers, cells, universes and their fractal relationships.
Prerequisite: [intention and governance](01-INTENTION-AND-GOVERNANCE.md).
Sources: S01, S03 and S04 in the [source map](../../review/SOURCE-MAP.md).

## In plain language

The rules explain what matters, the running system does the work, and the
interface helps people understand and control it. Two spaces sharing a machine
do not automatically share their data or permissions.

**[EXPLANATION S03]**
The layer and boundary explanations below do not define new jurisdiction rights.

## What is it?

Three layers answer different questions. OS states meaning, constraints and
proof obligations. Runtime performs effects, enforces current permissions and
preserves state. Workspace makes work understandable and usable. A host operating
system is another concern: SHAPER OS is not a mandatory Linux distribution.

Under the [25 October direction](../../decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md),
functional units (client term: components) form a generic stem cell; that base
plus one or more domain functional units forms a specialized cell (client term:
service). A universe (client term: space) is the logical sum of the cells of one
organization, with no outer container; earlier `univ-*` operational compositions
are read as cells or their classes under the
[27 October vocabulary direction](../../decisions/2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md). Fractal scope repeats intention, governance,
action and recovery with explicit boundaries and finite resource commitments.
The [composition owner projection](../architecture/COMPOSITION.md) distinguishes
this hierarchy from OS/Runtime/Workspace and from physical hosting.

## Why does it exist?

Meaning must survive replacement of code, host and interface. Containment must
not quietly imply access, and shared infrastructure must not imply shared data.
Separating these concerns lets the tandem change one realization without losing
the original purpose or confusing who is responsible for what.

## In practice

A universe contains a communications cell and an enterprise (CRM/ERP) cell. A
conversation reference may reach a customer record through a permitted exchange.
Being in the same universe does not let the enterprise cell read every conversation.
The Workspace displays the authorized reference; the Runtime enforces the
exchange; OS explains the sovereignty and evidence obligations.

Describe five relationships separately: logical containment, authority,
functional dependency, data ownership, and physical hosting. A unit running on
the same host as another gains no authority from that placement. Moving a host
does not by itself change the business jurisdiction.

## What can fail?

A screen hides an action while the backend still accepts it; a parent is assumed
to have unlimited child access; a universe (“space”) is confused with an object
index, UI folder or outer container; or a fractal analogy is used to justify unlimited recursion. Every
crossing needs an explicit contract, including parent/child crossings.

Logical containment can be a hierarchy, while functional relationships form a
graph. Do not force all five relationship types into one tree. A compromised
unit must not be the sole judge of its own recovery.

Read the [profile's scope-placement section](../profiles/SEPTEMBER-CONTAINER-MARIADB.md)
to connect cells to their base units. Functions owned at universe level,
actual door-ratification roles and permitted nesting of universes are declared by the
realization under the local [perimeters](../architecture/PERIMETERS.md) and
[topology](../architecture/TOPOLOGY.md) contracts. This chapter does not invent
a business hierarchy through a fractal analogy.

## How do we verify understanding?

Take two universes sharing a host and identify which data exchange is allowed,
who authorized it and what remains forbidden. Then move one universe's cells to
another host on paper. Explain which deployment assumptions require new proof and which
logical responsibilities remain unchanged.

Next: [the three frameworks](03-CREATION-EXECUTION-PROTECTION.md).
