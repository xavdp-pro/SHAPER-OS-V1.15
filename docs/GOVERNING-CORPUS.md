# Governing corpus — V1.15 editorial and operational boundaries

Purpose: connect the ready-to-use V1.15 framework, its editorial directions and
the versioned operational laws attached to concrete realizations.

## Adopted editorial directions

The [operator decision](../decisions/2026-09-23-AGNOSTIC-NO-CODE.md) records the
explicit English, generic, agnostic, code-free and pedagogical mandate. Its
source passages and interpretation limits are identified in that document.
[INTENT](../INTENT.md) applies that mandate to this edition's contents;
[AGENTS](../AGENTS.md) and the [reading contract](READING-CONTRACT.md) govern
work on these documents. This file defines their scope and precedence.

If editorial documents conflict, the operator's explicit instructions control;
their recorded decision is a restatement, not authority to alter the original.
INTENT applies that direction to the repository boundary. AGENTS, the reading
contract and this map organize work within it and cannot broaden its authority
or waive its limits. Record and resolve any remaining material conflict before
the affected action. Navigation and explanations do not override operational law;
current explicit operator decisions apply within their recorded construction
scope, as mapped below, without rewriting existing deployments.

These five documents are the **adopted editorial foundation**. Operational
realizations use their own identified governing corpus.
The six learning chapters, glossary, profile preservation note and worked examples
are explanatory or target-design documents with the status stated in each.
They are mandatory study material for the principal agent, not new runtime laws.

Later dated operator decisions record further scoped directions: the
[reference bridge decision](../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md)
and the [functional-unit MariaDB decision](../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md).
Each applies within the scope it states and, like the original direction,
controls conflicting editorial text within that scope. They do not enlarge the
editorial foundation above, seal successor law or certify a built artifact. The
[Reference Universe Procedure](procedures/01-REFERENCE-UNIVERSE.md) is an
editorial construction guide that records those directions.

The [2 October presentation decision](../decisions/2026-10-02-PRACTICAL-USE-AND-REFERENCE-SCENE.md)
establishes V1.15 as ready for use, with daily practical use by the operator. The
[ideal scene](IDEAL-SCENE.md) is an explanatory entrance and first exercise;
it does not extend operational authority. The remaining successor reconciliation
is an editorial scope, not a blanket status for the whole framework.

The [5 October first-construction decision](../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md)
clarifies that the agent generates implementation from the frame and that a
registry is recommended after reusable realizations exist. It applies to new
construction from zero and states its relationship to earlier registry wording.

## What governs operational work?

V1.15 is ready for use as the shared framework. Existing realizations retain
their versioned operational corpus: applicable LAW, RULES, intent, declared
composition and ratified decisions. The editorial crosswalk connects these
obligations across versions. This documentation edition carries the framework;
realization repositories carry the implementation and its contracts.

Before operational work, identify and record the target realization and the
exact governing revision attached to it. Do not use a moving branch, an old
local checkout or a newer explanatory chapter as silent replacement authority.
If the applicable revision or a material conflict cannot be resolved from the
target's records, pause the affected operational action and ask its authorized
owner. Reading and bounded documentation corrections may continue.

### Starting a new realization

When nothing exists yet, the agent creates the realization record instead of
waiting to find one. Record the human's intention and mandate, the V1.15 revision,
applicable dated decisions, the selected construction profile and the versioned
operating obligations used for this work. Follow the
[creation example](examples/CREATE-A-UNIVERSE.md) and
[reference procedure](procedures/01-REFERENCE-UNIVERSE.md) to generate and qualify
the implementation. A realization workspace can start empty.

Reading an external operational contract is distinct from importing or installing
the code beside it. For the current model, the preserved V1.14 sources can be
read at the fixed comparison revision below:
[LAW](https://github.com/xavdp-pro/SHAPER-OS-V1.14/blob/958e0b74e19af6ee833cba24fc31d1b866f6cf73/LAW.md),
[RULES](https://github.com/xavdp-pro/SHAPER-OS-V1.14/blob/958e0b74e19af6ee833cba24fc31d1b866f6cf73/software/RULES.md)
and [boot contract](https://github.com/xavdp-pro/SHAPER-OS-V1.14/blob/958e0b74e19af6ee833cba24fc31d1b866f6cf73/docs/agent/BOOT-CONTRACT.md).
If the repository preview truncates a document, read its complete plain-text
version: [LAW text](https://raw.githubusercontent.com/xavdp-pro/SHAPER-OS-V1.14/958e0b74e19af6ee833cba24fc31d1b866f6cf73/LAW.md),
[RULES text](https://raw.githubusercontent.com/xavdp-pro/SHAPER-OS-V1.14/958e0b74e19af6ee833cba24fc31d1b866f6cf73/software/RULES.md)
and [boot-contract text](https://raw.githubusercontent.com/xavdp-pro/SHAPER-OS-V1.14/958e0b74e19af6ee833cba24fc31d1b866f6cf73/docs/agent/BOOT-CONTRACT.md).
Follow their applicable references, compare the later scoped decisions, and
record the obligations used; a comparison revision is not automatically every
existing deployment's revision.

The agent fills in implementation details and writes concrete unit contracts
that satisfy the known obligations. An absent schema, internal API or build
recipe is implementation work. An unknown authority, contradictory requirement
or undecided business policy is a specific decision gap. Identify and resolve
that gap before its dependent action while continuing independent authorized
work. Do not turn all open editorial items into a prerequisite for every build;
for example, an isolated single-universe exercise need not decide doors between
two jurisdictions or recursive space composition.

### Current construction crosswalk

**[MANDATE: scoped operator directions]** For a new construction requested under
this model, apply the decisions below when reading the older comparison corpus.
This resolves the stated differences; it does not give explanatory chapters
permission to waive unrelated obligations.

| Older comparison wording | Meaning for this new construction | Owning direction |
| :--- | :--- | :--- |
| Rule 3 makes the machine registry a prerequisite. | Generate and verify the first implementation without a pre-existing registry; recommend it later for repeatable distribution. | [5 October construction decision](../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md) |
| Rule 11 records nested recipes as unproven in that tree. | Retain the nested system-container universe. The operator reports repeated practical deployment, including nested Podman; qualify this new candidate on its selected host. The old dated observation is not a present prohibition. | [6 October clarification](../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md) |
| Rules 0H/7 keep the cognition core provider-neutral. | Keep the shared bridge intent generic and use OpenCode in this selected reference composition. A scoped adapter choice is not a universal provider law. | [24 September reference decision](../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md) and [common bridge intent](intents/cognition-bridge.md) |
| Rules 4/26 require private MariaDB per functional unit. | Preserve separate MariaDB instances from first construction; no shared development database or substitute engine. | [24 September storage decision](../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md) |
| The boot contract stops work on missing required secrets or blocked authority. | Generate implementation and prepare independent units within the existing mandate. Resolve a genuinely missing dependency before exercising its dependent action; do not demand unrelated production credentials for a local build. | [5 October construction decision](../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md) |
| A CLI may impose its own interactive approval or sandbox default. | In mandated DEV, implement full noninteractive execution without CLI sandbox or repeated approval questions; report a concrete adapter gap if that mode is unavailable. | [6 October execution direction](../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md#mandated-development-execution) |

The construction agent records this applied crosswalk in the new realization
and writes its concrete contracts. A missing recipe is construction work. An
unresolved business policy or authority conflict is a different, specific gap.
Existing deployments retain their governing records and require their own
migration scope; this table does not claim that they were rewritten or retested.

### Fixed comparison reference

For successor reconciliation, the fixed V1.14 comparison reference is
`958e0b74e19af6ee833cba24fc31d1b866f6cf73`, including `LAW.md`,
`software/RULES.md` and their required governing references. On 27 September
2026, Codex read `LAW.md`, all of `software/RULES.md` (lines 1–1559), and
`docs/agent/BOOT-CONTRACT.md` in full at that exact reference. Supporting
coverage and remaining sources are recorded in the
[reading ledger](../review/READING-LEDGER.md#operational-law-reading--27-september-2026).
The core operational texts have been read; complete coverage of their linked
corpus and rule-by-rule successor mapping remain open. Earlier readings at
`c88fd8742f5ed93a7fdcc3b342cf8580a4e37d17` are not equivalent coverage. Neither
reference is asserted to describe every deployed artifact's governing revision.

The preserved September target has its own
[applicability boundary](profiles/SEPTEMBER-CONTAINER-MARIADB.md). Existing
prototype gaps are not exceptions that weaken the target, and a target note is
not evidence that an old runtime has already been rebuilt.

## Finite reading set

For this correction checkpoint, these groups define the principal agent's
required coverage, not a second reading order. Enter through the board and follow
its navigation, including prerequisites and the common learning sequence:

1. The five editorial-foundation documents listed above.
2. The [practical-use decision](../decisions/2026-10-02-PRACTICAL-USE-AND-REFERENCE-SCENE.md)
   and [ideal scene](IDEAL-SCENE.md), then the later scoped decisions listed above, the
   [reference bridge](../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md) and the
   [functional-unit MariaDB](../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md),
   the [first-construction decision](../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md),
   the [deployment and continuity clarification](../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md),
   the [creation example and prerequisites](examples/CREATE-A-UNIVERSE.md),
   and the [Reference Universe Procedure](procedures/01-REFERENCE-UNIVERSE.md).
3. [Board](CONTEXT-INDEX.md), [glossary](GLOSSARY.md) and
   [artifact vocabulary](architecture/VOCABULARY-BOUNDARY.md).
4. All six numbered learning chapters linked by the board, in order.
5. [September target profile](profiles/SEPTEMBER-CONTAINER-MARIADB.md) and the
   [realization intents](intents/README.md): the
   [generic cognition bridge](intents/cognition-bridge.md),
   [OpenCode profile](intents/cognition-bridge-opencode.md) and
   [Meta Muse profile](intents/cognition-bridge-meta-muse.md).
6. [Human guide](human/READING-GUIDE.md), [self-checks](human/METACOGNITION.md),
   [medium route](agent/MEDIUM.md) and [strong route](agent/STRONG.md).
7. [Scenario checks](examples/COMPREHENSION-CHECKS.md) and
   [worked answers](examples/WORKED-ANSWERS.md).
8. [Source map](../review/SOURCE-MAP.md), [ledger](../review/READING-LEDGER.md),
   [continuity protocol](../review/VERIFICATION-AND-CONTINUITY.md) and the
   [correction record](../review/OPUS-CORRECTIONS-2026-09-23.md).

The README is an entrance; the earlier reading-structure review is historical
evidence, not an additional law. Operational tasks additionally require the
exact external governing corpus and affected unit contracts. The unresolved
external reading inventory is tracked separately; this finite study set is not
a claim to have enumerated or reconciled every ecosystem source.

## Meaning of “complete foundation”

For practical work, that phrase means the finite study set **plus the identified
operational corpus of the chosen realization**, recorded by the agent when it
creates a new one. The editorial crosswalk keeps
obligation ownership visible across versions. Evolve this map into an explicit
adopted-law index as that crosswalk progresses, preserving each obligation.
