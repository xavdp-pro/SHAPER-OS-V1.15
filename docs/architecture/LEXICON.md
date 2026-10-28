# Operational language and canonical vocabulary

The [independent glossary](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md)
owns stable shared concept IDs. This local page projects their operational use
under [Rule 37](../../RULES.md#rule-37); [composition](COMPOSITION.md) connects
micro and macro scales. Existing identifiers retain compatibility. Agent-facing
prose leads with the technical terms below and human-facing prose with their
client terms, under the [27 October vocabulary direction](../../decisions/2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md);
“brick/brique” remains a compatibility alias.

## The three grammar rules

1. A class is a reusable versioned definition; specialization records inherited
   obligations and domain deltas; an instance has its own stable identity/state.
2. Position and lineage live in structured records, independently of the slug.
3. Product source and its private `-lab` companion have separate custody. A
   repository's name does not determine runtime identity or cardinality.

## Compatible prefixes

[NAMING](NAMING.md) preserves `univ-`, `brick-`, `pkg-`, `img-`, `ctr-`, `vol-`,
`cfg-`, `ctx-`, `task-` and `proof-` identifiers. The `univ-<project>-<class>`
grammar applies to its existing class-repository lineage; other source roles
have names that identify their ownership. Renames use explicit mappings.

## Operational terms

| Term | Local contract and owner |
| --- | --- |
| Functional unit — FUnit, organelle (client: component) | Bounded function, interfaces, lifecycle and private MariaDB; [Rules 4/26](../../RULES.md) |
| Generic stem cell | Reusable base cell; [profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md) |
| Specialized cell (client: service) | Base plus one or more domain functional units; its owning domain contract |
| Universe (client: space) | Logical sum of the cells of one organization, without physical envelope; earlier single-composition uses are read by their content; [composition](COMPOSITION.md) |
| Supervision cell (client: cockpit) | Reads several universes by pull or published events; never in their transactional path |
| Class / specialization / instance | Reusable definition / declared derivation / stable materialization; [composition](COMPOSITION.md) |
| Ledger | Governor-owned desired instance state in private MariaDB; [governor](../contracts/governor.md) |
| Drift | Observed difference from desired state; bounded reconciliation under Rule 27 |
| PURRING / DEGRADED / REAPED | Dated protocol states; exact eligible transitions and retry bounds belong to the governor contract |
| status.json | Canonical exported status surface derived from authoritative MariaDB; no rival file-based application store |
| Board | Runtime view of dated status for the authorized scope; the documentation board is navigation |
| Fleet map | Pinned reusable definitions and host capabilities, not instance state; [fleet](FLEET.md) |
| Forge | `brick-forge` lifecycle function for declared functional units inside its scope; never authority over its own vital substrate |
| forkedFrom | Versioned lineage fields for package and repository compatibility |
| Mirror rule | Preserved Rule 33 fork naming convention in that lineage; source ownership remains explicit |
| source / perimeter | Provenance and P1/P2/P3 functional classification; neither is OS/Runtime/Workspace or ownership |
| Governor — public root cell (client: guichet, its request interface) | Scoped desired-state owner; delegates through the declared protocol, without host keys |
| Maker — private root cell (client: fabrication workshop) | Enrolled deterministic host actor; typed frozen recipes, observed effects and bounded lanes; [maker](../contracts/maker.md) |
| Matrix | Locked content-addressed artifact selected from versioned class sources |
| Rig | Delivered composition of pinned classes, functional units and declarations |
| Tool | Typed capability available to an agent within its human-approved action policy |
| Bridge | Neutral cognition/execution capability contract; OpenCode is the default reference adapter |
| Helm | Human conversational interface requesting governed work; UI does not grant authority |
| Jurisdiction | Declared responsibility and allowed action; shared membership or placement grants no additional rights |
| Root | Human–AI tandem authority within a declared jurisdiction; infrastructure and client responsibilities remain distinct |
| Pilot level | Validated ability for a class under the existing E0–E5 profile; competence and mandate remain distinct |
| Shape | Declared `direct`, `lxc` or `nested` hosting profile; old profile defaults remain tied to their versions |

## Operations and retrieval

Creation, verification, deployment, capture/restore and recovery retain their
owners and typed meanings. Start from [source roles](SOURCE-ROLES.md) for the
exact task route, then follow dependencies and reverse references. Full reading
uses the [board](../CONTEXT-INDEX.md). One source owns each definition; local
interpretations identify their scope instead of silently creating a rival canon.
