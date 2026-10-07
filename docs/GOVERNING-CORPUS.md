# Governing corpus — self-contained SHAPER OS V1.15

Purpose: identify the complete local framework, its authority, reading sequence
and contract owners. No other SHAPER OS edition is required.

## Authority and ownership

The [human direction adopting this corpus](../decisions/2026-10-06-SELF-CONTAINED-CORPUS.md)
makes the local [LAW](../LAW.md), [RULES](../RULES.md) and their contract dependencies
the operational frame of this edition. Rule identifiers remain stable. Laws state
obligations; contracts make their state, interfaces, lifecycle and evidence precise.
Learning chapters and examples explain them without replacing or waiving them.

The human controls the mandate and changes of direction. [INTENT](../INTENT.md)
owns the repository boundary; [AGENTS](../AGENTS.md) and the
[reading contract](READING-CONTRACT.md) organize work within it. A later date or
an assistant proposal alone cannot alter a rule. A scoped explicit human decision
applies only to its recorded subject. Resolve a real conflict at its owner and
record the result before the action that depends on it.

The current construction directions are local:

- [Code-free, generic framework](../decisions/2026-09-23-AGNOSTIC-NO-CODE.md).
- [OpenCode reference composition](../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md).
- [Private MariaDB per functional unit](../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md).
- [Practical use and ideal scene](../decisions/2026-10-02-PRACTICAL-USE-AND-REFERENCE-SCENE.md).
- [First construction and later registry reuse](../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md).
- [Practical deployment, bridge continuity and DEV/production policy](../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md).
- [Self-contained local corpus](../decisions/2026-10-06-SELF-CONTAINED-CORPUS.md).

## Mandatory local operational corpus

Read [LAW](../LAW.md) and [RULES](../RULES.md) in full, including the preamble and
all rule sections. Also read the [boot contract](agent/BOOT-CONTRACT.md),
[operating contract](agent/OPERATING-CONTRACT.md),
[proof contract](agent/PROOF.md) and [lifecycle contract](agent/LIFECYCLE.md).
Then follow their local contract dependencies for the intended composition.
A reading board, crosswalk, summary or earlier review is not a substitute.

The architecture is defined locally by [perimeters](architecture/PERIMETERS.md),
[topology](architecture/TOPOLOGY.md), [cognition](architecture/COGNITION.md),
[naming](architecture/NAMING.md), [lexicon](architecture/LEXICON.md) and
[fleet](architecture/FLEET.md). These explain authority, placement and relations,
not a pre-existing infrastructure the reader must find.

For the reference universe, read each unit's contract:
[Vault](contracts/vault.md), [Logger](contracts/logger.md),
[Queue](contracts/queue.md), [Maestro](contracts/maestro.md), the
[generic cognition bridge](intents/cognition-bridge.md), its
[transport/status contract](contracts/bridge-status.md) and the
[OpenCode profile](intents/cognition-bridge-opencode.md).
For fractal deployment work, read [governor](contracts/governor.md),
[maker](contracts/maker.md) and [maker recipes](contracts/maker-recipes.md).
They are local meanings and obligations from which an agent generates code.

The supporting design contracts are [consulted context](design/CONSULTED-CONTEXT.md),
[document pipeline](design/DOCUMENT-PIPELINE.md) and
[cooperative ecology](design/COOPERATIVE-ECOLOGY.md). Consult the relevant owners
before delegating cognition or processing documents; full rule reading remains
mandatory even when a specialist contract is irrelevant to the current task.

## Adoption in an existing project

[LAW owns the two uses, explicit adoption and binding scope](../LAW.md#two-uses-and-explicit-adoption).
The [agent entrance](../AGENTS.md) and [boot contract](agent/BOOT-CONTRACT.md#2-establish-the-mandate-and-work-perimeter)
apply that contract to ongoing development without imposing a new construction.
Use the [ongoing-project alignment prompt](examples/PROJECT-STANDARD-ADOPTION.md#prompt-align-an-ongoing-project)
to begin adoption, then the same example's record to identify the selected corpus,
actual scope and existing gaps in project instructions.
The mandatory reading above still applies; this route is not a reduced rulebook.

## Starting a new realization

An empty workspace is a valid starting point. Record the human's intention,
mandate, this repository revision, selected profile, applicable decisions and
required evidence in the new realization. Use the
[creation request and prerequisites](examples/CREATE-A-UNIVERSE.md) and
[reference procedure](procedures/01-REFERENCE-UNIVERSE.md) to produce the
implementation in a separate workspace. Neither an existing SHAPER executable,
image, realization repository nor registry is needed to begin.

The constructor fills in implementation details and writes concrete contracts
that satisfy the local obligations. An absent build recipe, internal schema or
implementation is work to do. An unknown authority or business policy is a
specific decision gap; resolve it before its dependent action while continuing
independent authorized work. Do not demand unrelated production credentials for
a DEV build or decide cross-jurisdiction policy for an isolated base universe.

Existing realizations carry their own versioned composition, implementation and
operating records. Inspect those when acting on such a system. Documentation
consolidation does not migrate a deployment or prove that its configuration changed.

## Current construction crosswalk

This table connects current choices to their local owners. It does not replace
reading those owners and is not a licence to waive unrelated obligations.

| Subject | Current obligation | Owning documents |
| :--- | :--- | :--- |
| First implementation | The agent generates code from intentions; registry reuse follows verified construction. | [Rules](../RULES.md), [construction direction](../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md) |
| Containment | An outer system-container universe contains its Podman functional units; a flat host network is not an alternative to this model. | [Rules](../RULES.md), [current profile](profiles/SEPTEMBER-CONTAINER-MARIADB.md) |
| State | Each functional unit owns a private MariaDB instance and its own durable state. | [Rules](../RULES.md), [storage direction](../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md) |
| Cognition | Shared context/session/action obligations are provider-neutral; the reference selects OpenCode. | [Common bridge](intents/cognition-bridge.md), [OpenCode](intents/cognition-bridge-opencode.md) |
| DEV execution | Full noninteractive execution within the human mandate, without obstructive CLI sandbox or repeated approvals. | [Execution and security direction](../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md) |
| Production | The tandem implements proportionate action/type permissions after functional integration and rechecks the accepted workflows. | [Shared security lifecycle](intents/cognition-bridge.md#security-by-design-followed-by-a-dedicated-hardening-phase) |
| Qualification | Observe real effects, persistence, recovery and refusal boundaries; a transcript or health endpoint is not business proof. | [Proof](agent/PROOF.md), [unit contracts](contracts/queue.md) |

## Finite reading set

Enter through the [board](CONTEXT-INDEX.md). Principal agents share the same
foundation; medium and strong routes differ in reasoning support, not permissions.
The complete local foundation comprises:

1. [INTENT](../INTENT.md), [AGENTS](../AGENTS.md), this map, the
   [reading contract](READING-CONTRACT.md), and the scoped decisions listed above.
2. The mandatory local operational corpus and its architecture/contracts listed above.
3. [Ideal scene](IDEAL-SCENE.md), [glossary](GLOSSARY.md),
   [artifact vocabulary](architecture/VOCABULARY-BOUNDARY.md), and the six learning
   chapters linked by the board, in order.
4. [Current profile](profiles/SEPTEMBER-CONTAINER-MARIADB.md),
   [creation example](examples/CREATE-A-UNIVERSE.md),
   [reference procedure](procedures/01-REFERENCE-UNIVERSE.md), and relevant
   [adapter profiles](intents/README.md).
5. [Human guide](human/READING-GUIDE.md), [self-checks](human/METACOGNITION.md),
   [medium route](agent/MEDIUM.md), [strong route](agent/STRONG.md),
   [scenario checks](examples/COMPREHENSION-CHECKS.md) and
   [worked answers](examples/WORKED-ANSWERS.md).

Before concrete work, follow and read the detailed local dependencies applicable
to it, record exact coverage and explain the meaningful contract. Unread material
is not silently treated as known. Runtime configuration, vendor manuals and the
human's business-specific intentions are supplied by the chosen realization;
they are not missing SHAPER editions.

## Maintenance and review records

The [current source/owner map](../review/SOURCE-MAP.md) and
[ledger](../review/READING-LEDGER.md) track this corpus. The
[continuity protocol](../review/VERIFICATION-AND-CONTINUITY.md) defines reading and
verification records. Historical [structure review](../review/READING-STRUCTURE-REVIEW.md)
and [correction checkpoint](../review/OPUS-CORRECTIONS-2026-09-23.md) are optional
maintenance context, never governing prerequisites or substitutes for current law.

Being self-contained is a documentary property. Each constructed realization
still proves its actual source, configuration, effects, restoration and acceptance.
