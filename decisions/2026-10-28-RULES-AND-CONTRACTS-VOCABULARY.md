# Rules and contracts vocabulary — 28 October 2026

Authority: explicit human direction of 28 October 2026. Scope: how the rules,
contracts, procedures and agent contracts of this edition read “universe” under
the [27 October vocabulary direction](2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md).
No identifier, anchor, path, manifest field, protocol value or rule title is
renamed by this record. Earlier decisions keep their dates and wording.

## Each use shifted to its level

| Earlier use of “universe” | Reading now |
| --- | --- |
| One operational composition, its definition or its manifest | cell, generic or specialized by its content; its repository is a class repository |
| A running dev, test or prod environment, a ledger row, what a maker stamps, reaps or restores | cell instance |
| An organization's or client's space | universe |
| A statement true at both scales | cell or universe |
| The parent in the lifecycle tree | parent level (K+1) |

Rules keep the shorter “instance” where the cell is clear from context.

[Procedure 01](../docs/procedures/01-REFERENCE-UNIVERSE.md) builds the reference
stem cell: the generic stem cell with its base units and default bridge, without
project-specific function. Deriving from it instantiates a cell with fresh
identity, credentials, state and storage. A specialized cell adds its declared
domain units; instantiation alone never specializes it.

The governor is a public root cell; its ledger lives in its governor unit's
private database. Makers stamp and reap cell instances. Several scoped
governors remain allowed, and no organization must acquire a governor of its own.

## Laws clarified

- **Lifecycle tree.** The levels K, K+1 and N of Rules 23–25 and 36 count
  lifecycle authority: who repairs, updates, creates and ends whom. They are not
  the composition levels 0–4. An instance's parent level is its governor and the
  makers that governor enrolled; the governor writes desired rows and the maker
  alone holds host capability. The root universe of
  [Rule 24](../docs/rules/05-REPAIR-AND-DATA.md#rule-24) is the master root's own
  universe, whose root cells have no parent. Universes never contain universes.
- **Jurisdiction.** A jurisdiction covers universes and may be narrowed to some
  cells within a universe. Neither universe membership nor jurisdiction grants
  host, governor or maker power.
- **Data lifecycle.** Each cell declares its data lifecycle; its termination
  clause applies when a cell instance is decommissioned. Erasing a client's data
  covers every store of every cell of that client's universe. A universe's policy
  is the sum of its cells' declarations.
- **Isolation.** A query stays within the cell, universe or tenant scope it is
  authorized for; a client's universe never widens a cell-scoped authorization.
- **Blank universe.** The offer keeps its name. It grants a bare cell instance,
  without class content, to an infrastructure client.

## Placement tools

PodMesh keeps the name `universe` for the runtime unit it places, moves and
captures. The realization declares what that unit contains: functional units, a
cell instance, or the cells of a universe given shared storage.

## Kept identifiers

`ctx-universe.md` describes the agent's cell and names its universe. The literal
header `SPECIFIC INTENT (Universe: <univ_slug>)` keeps its word; `<univ_slug>`
names the specific cell. Procedure 01 keeps its file name; rule titles, including
those of Rules 1 and 31, and every anchor keep their identities. Where an agent
reading a single page could misread a kept identifier, a short note stands there.
