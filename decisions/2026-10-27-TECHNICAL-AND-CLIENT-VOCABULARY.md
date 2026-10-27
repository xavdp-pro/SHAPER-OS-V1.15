# Technical and client vocabulary — 27 October 2026

Authority: explicit human direction of 24–27 October 2026. Scope: the vocabulary
of this edition and how its readers interpret it. No identifier, image, path,
manifest field, protocol value or rule anchor is renamed by this record. Earlier
decisions keep their dates and wording; this record supersedes the 25 October
preference for “component” in agent-facing prose and the earlier picture of a
space containing universes.

## One scale, two registers

The human–AI tandem uses one composition scale with two registers. Agent-facing
sources lead with the technical term, so an agent that reads a single page still
meets the exact concept. Human-facing explanations lead with the client term.
The first use of a term in a page pairs both.

| Level | Technical term (agent-facing) | Client term (human-facing) | Meaning |
| --- | --- | --- | --- |
| 0 | process, binary | — | Executable material beneath a functional unit; engineering detail, outside client vocabulary. |
| 1 | functional unit (FUnit, organelle) | component | One bounded responsibility with its identity, private state, interface and lifecycle. |
| 2 | cell: generic stem cell, specialized cell | service | The stem cell is the reusable base cell. A stem cell plus one or more domain functional units forms a specialized cell, for a business, support or transversal purpose. |
| 3 | universe | space | The logical sum of the cells of one organization, enterprise, shop or project. |
| 4 | supervision cell | cockpit | A cell that reads the state of several universes. |
| fabrication | governor, public root cell | guichet, its request interface | Owns approved desired state and receives requests; holds no host power. |
| fabrication | maker, private root cell | fabrication workshop | Claims approved work, applies frozen recipes that instantiate and specialize cells, and attaches them to a universe. |

“Fabrication workshop” is never shortened: in the independent glossary,
“workshop” names a `-lab` work repository. A root cell serves the construction
of the fractal; it is not root authority, which remains with the tandem under
[Rule 37](../docs/rules/07-TREE-AND-FLEET.md#rule-37).

## Laws attached to the scale

- A universe has no physical envelope. Its membership is declared in its
  governor's records; each cell keeps its own runtime boundary and private
  state. A realization may give a universe shared storage or IPC jurisdiction,
  for example to capture or move its cells together; that is a profile choice,
  outside the logical definition.
- A supervision cell observes by pull or by consuming published events. It never
  enters a universe's transactional path, and its failure or relocation never
  stops a universe.
- Governors and makers keep the separation of the
  [governor](../docs/contracts/governor.md) and [maker](../docs/contracts/maker.md)
  contracts: the governor writes desired state and holds no host key; the maker
  acts on its own host from frozen recipes and reports observed facts.

## Reading earlier sources

Earlier texts used “universe” for one operational composition, often a single
service, and described a space containing universes. Read each such use by its
actual content: usually a specialized cell, its class or its instance. `univ-*`
repositories, the manifest `universe` field, `<univ>/` paths, `brick-*` names,
rule anchors and protocol fields keep their identities until their owners
authorize a versioned migration with explicit mappings. The
[independent glossary](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md)
keeps its stable concept IDs; this edition links them.

## Naming grammar

[Rule 1](../docs/rules/02-CONSTRUCTION.md#rule-1)'s grammar reads
`univ-<project>-<class>` in English. It follows the programming metaphor of a
class and its instantiation: the repository defines the class; each instance
materializes it with its own identity, environment and state (`<slug>-dev`,
`<slug>-test`, `<slug>-prod`).

## Owning pages

The [working glossary](../docs/GLOSSARY.md), [composition](../docs/architecture/COMPOSITION.md),
[lexicon](../docs/architecture/LEXICON.md), [vocabulary boundary](../docs/architecture/VOCABULARY-BOUNDARY.md),
[naming](../docs/architecture/NAMING.md) and Rule 1 apply this record. Where a
page still uses an earlier sense, the reading rule above applies.
