# Internal reading board

Status: reading structure populated; successor law reconciliation still open.
Read this map before narrowing to a component.
The source coverage and open work are recorded in the
[reading ledger](../review/READING-LEDGER.md). This board is a map, not a second
copy of the law and not a deployment-status database.

## Orientation — shared by humans and agents

1. [Governing corpus](GOVERNING-CORPUS.md): the finite study set, editorial authority
   and the operational laws that this candidate does not replace. Then
   [Intent](../INTENT.md): purpose, agnosticism, code-free boundary and completion.
2. [Current decision](../decisions/2026-09-23-AGNOSTIC-NO-CODE.md): what the human
   has explicitly requested for the successor. The later
   [reference bridge decision](../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md)
   selects OpenCode for the proposed reference composition. The
   [functional-unit MariaDB decision](../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md)
   states that every next unit under the current model owns a private MariaDB,
   with existing SQLite prototypes kept as separate, declared debt.
3. [Reading contract](READING-CONTRACT.md): document authority, comprehension
   and continuity after context loss.
4. [Glossary](GLOSSARY.md): first meanings, then the
   [vocabulary boundary](architecture/VOCABULARY-BOUNDARY.md) for package/brick/unit.
5. Choose the [human guide](human/READING-GUIDE.md),
   [medium agent route](agent/MEDIUM.md) or [strong agent route](agent/STRONG.md).
   Human depths select an appropriate subset from the shared material. Agents
   read the complete finite study set; they do not skip its foundation.

## Common learning sequence

1. [Intention and governance](learning/01-INTENTION-AND-GOVERNANCE.md): distinguish
   information, interpretation, mandate, action and result. Required before all
   later chapters. Check: what does a price-update request actually authorize?
2. [Layers and scopes](learning/02-LAYERS-AND-SCOPES.md): OS/Runtime/Workspace,
   space/universes and fractal relationships. Builds on 1; informs boundaries in
   3 and dependencies in 4. Check: does a shared host grant shared data access?
3. [Creation, execution and protection](learning/03-CREATION-EXECUTION-PROTECTION.md):
   what is intended, what runs, what controls crossings. Builds on 2; supplies
   unit obligations in 4. Check: what survives replacement of an instance?
4. [Units and dependencies](learning/04-UNITS-AND-DEPENDENCIES.md): state owners,
   exchanges, receipts, failure and the September target. Builds on 3; constrains
   realization in 5. Check: who owns an effect after a worker loses its lease?
5. [Materialization](learning/05-MATERIALIZATION.md): generic contracts, scoped
   concrete choices, separate implementation and deployability obligations.
   Builds on 1–4; requires evidence from 6. Check: what must a code replacement
   preserve besides its interface?
6. [Evidence, recovery and learning](learning/06-EVIDENCE-RECOVERY-LEARNING.md):
   real effects, observers, restoration and correction. Builds on 1–5; sends
   feedback back to intention and design. Check: what does a receipt not prove?
7. [Human and agent self-checks](human/METACOGNITION.md): different practical
   checks for the same discipline, including correction of the correction system.
8. [Comprehension scenarios](examples/COMPREHENSION-CHECKS.md): apply the whole
   chain to new conditions; conceptual success is not runtime qualification.
   Compare the [worked answers](examples/WORKED-ANSWERS.md) at human and agent depths.

After chapter 4, read the [September target profile](profiles/SEPTEMBER-CONTAINER-MARIADB.md)
for explicit applicability, unit placement and the remaining structural questions.

Each chapter answers what, why, practice, failure and verification. The sequence
teaches the frame; it does not substitute for the detailed adopted laws and unit
contracts that are still being reconciled.

## Use the board during work

- An unclear word: [glossary](GLOSSARY.md), then its owning chapter.
- An authority question: [governance](learning/01-INTENTION-AND-GOVERNANCE.md).
- A crossing or isolation question: [scopes](learning/02-LAYERS-AND-SCOPES.md)
  and [protection](learning/03-CREATION-EXECUTION-PROTECTION.md).
- A dependency or receipt question: [units](learning/04-UNITS-AND-DEPENDENCIES.md).
- A concrete technology or deployment question:
  [materialization](learning/05-MATERIALIZATION.md), then the external realization's
  own contract. For a new universe, use the proposed
  [reference-universe procedure](procedures/01-REFERENCE-UNIVERSE.md).
  This OS repository contains no executable runbook.
- A disagreement, missing observation or recurring failure:
  [self-checks](human/METACOGNITION.md) and [evidence](learning/06-EVIDENCE-RECOVERY-LEARNING.md).
- A provenance or completeness question: [source map](../review/SOURCE-MAP.md)
  and [ledger](../review/READING-LEDGER.md).

## After reading

Human readers explain the example at the depth they need. Principal agents
record exact reading coverage, answer all scenarios, locate the governing
requirements and list unresolved gaps before directing a concrete realization.
Use [review results](../review/READING-STRUCTURE-REVIEW.md) to distinguish checks
already performed from work that remains open.
The [Opus correction record](../review/OPUS-CORRECTIONS-2026-09-23.md) is the later
checkpoint; [continuity](../review/VERIFICATION-AND-CONTINUITY.md) specifies external
reading records, file digests and repeatable verification.

## Topics that must be covered by the completed board

- Governance: intention, observation, interpretation, uncertainty, mandate,
  START/CHANGE/STOP, evidence, learning and explicit revision.
- Pedagogy: words, gradient, reality; the five questions; five human reading
  levels; medium and strong agent comprehension.
- Scale: space containing universes; relationships among universes; recursive
  structure and limits; distinguish containment, authority and physical hosting.
- Responsibilities: OS, Runtime and Workspace; creation, execution and protection
  frameworks; functional units; declared exchanges and data ownership.
- Materialization: interpretation, packages, bricks, composition, deployment,
  verification, supervision, migration, recovery and replacement.
- Interdependencies: providers/consumers, startup, authority, state, receipts,
  idempotency, degraded behavior, cycles and restoration order.
- Ecosystem: the public site and the two wiki audiences, Enterprise and Helm,
  PodMesh capabilities and evidence, operational realization profiles.
- Lineage: earlier laws, adopted decisions, proposals,
  open contradictions and evidence with date and revision.

These topics are a completion checklist, not claims that their full successor
contracts already exist. Future board entries must link the owning documents,
prerequisites, affected neighbors and the scenario proving understanding.
