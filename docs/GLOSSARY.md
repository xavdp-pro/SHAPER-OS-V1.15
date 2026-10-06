# Working glossary

Purpose: explain the vocabulary used to understand and apply SHAPER OS.
Definitions follow the local [source and owner map](../review/SOURCE-MAP.md).
Definitions are **EXPLANATION**, except terms explicitly labeled **TARGET**.

## Understanding and authority

- **Intention:** the desired meaningful result, including constraints and who it
  serves; not merely a command to maximize a number.
- **Observation:** what a source or sensor reports under stated conditions.
- **Interpretation:** a proposed meaning of observations, open to challenge.
- **Tension:** a meaningful discrepancy that warrants attention, not its diagnosis.
- **Mandate:** permission for an actor to pursue a bounded result under conditions;
  technical ability and intelligence do not create it.
- **Standing mandate:** an explicitly authorized recurring scope with conditions,
  review and revocation; repetition alone does not create it. See
  [governance](learning/01-INTENTION-AND-GOVERNANCE.md).
- **START / CHANGE / STOP:** begin an action, change the method or end the activity
  according to evidence and authority; stopping does not necessarily undo an
  already completed effect. See [governance](learning/01-INTENTION-AND-GOVERNANCE.md)
  and the [operating contract](agent/OPERATING-CONTRACT.md).
- **Principal agent:** the agent coordinating understanding with the human and
  connecting affected contracts; a responsibility, not an automatic root identity.
  See the [agent routes](agent/STRONG.md).
- **Adopted editorial foundation:** the five editorial documents
  enumerated in the [governing corpus](GOVERNING-CORPUS.md), not all operational law.
- **Finite study set:** the larger enumerated reading set in that map, including
  explanatory chapters, examples and reviews; inclusion does not confer law status.
- **Proof:** evidence sufficient for a specific claim under declared conditions,
  not a claim of absolute certainty or of unrelated capabilities.
- **Metacognition:** examining how one forms judgments and chooses actions.
- **Meta-regulation:** examining and improving the sensors, review and correction
  mechanisms themselves through authorized change.
- **Proportionate response:** selecting an allowed response using current evidence,
  consequences of action/inaction and reversibility, without overreach or blanket
  refusal. See the [practical self-checks](human/METACOGNITION.md), source S09.
- **Work pacing:** adjusting the purpose and method of work to new information,
  declared deadlines and handoff/resumption conditions; not a universal sequence
  of Runtime states. See the practical self-checks, source S09.
- **Context-qualified lesson:** a revisable conclusion with stated applicability
  and review conditions, distinct from the observation it explains. See the
  practical self-checks, source S09.

## Layers and scopes

- **SHAPER OS:** generic intentions, principles, laws and contracts; no executable
  implementation. See [layers and scopes](learning/02-LAYERS-AND-SCOPES.md).
- **Runtime:** the realization that enforces permissions, preserves operational
  state and performs declared effects.
- **Workspace:** the human interaction surface over those capabilities; displaying
  an action is not authorizing it.
- **Space:** here, the containing scope for several universes, following the
  current operator direction. It is not automatically a filesystem folder,
  physical host or global access grant. Historical uses need explicit mapping.
- **Universe:** a bounded context with declared identity, responsibilities, state
  and exchanges. Its logical boundary and physical placement are different.
- **Fractal:** a pattern that can recur across scopes with explicit boundaries
  and adapted responsibilities, not a requirement for identical nested stacks.
- **Door:** a declared controlled crossing with callers, purpose, permitted data,
  receiving authorization, refusal and evidence semantics. It is not merely a
  network port or a Cognition Bridge. See [scopes](learning/02-LAYERS-AND-SCOPES.md)
  and the local [perimeter contract](architecture/PERIMETERS.md). The realization
  identifies the actual authorized roles and approval evidence.

## Construction and realization

- **Creation Framework:** the enduring specification of what is to exist and why.
- **Execution Framework:** the declared conditions that host and constrain its
  operational instance.
- **Protection Framework:** the identities, permissions, controlled crossings,
  refusals, containment and recovery protecting the system.
- **Functional unit:** a bounded responsibility with identity, owned state,
  declared contracts, lifecycle and proof obligations.
- **Brick / brique:** retained vocabulary for a deployable realization. In the
  [September target profile](profiles/SEPTEMBER-CONTAINER-MARIADB.md) it is an
  image/container with a declared function.
  The OS describes the contract, not the image or its implementation code.
- **Implementation package:** reusable source used to build a realization,
  without its own independent deployment lifecycle. See the local
  [naming contract](architecture/NAMING.md).
- **Organizational pack:** an initial domain composition of concepts, workflows
  and policies. Some older Runtime documents also call this a package. Always
  qualify which sense is intended; do not equate it to an implementation package.
- **Realization profile:** an explicitly scoped set of concrete technology and
  deployment choices satisfying the generic contracts; not a loophole for
  weakening them. See [materialization](learning/05-MATERIALIZATION.md).
- **Realization repository:** the separately governed home of concrete code,
  executable artifacts, deployment recipes and their tests. The construction
  agent creates it when starting from zero; it is an output of the work, not a
  required pre-existing codebase. See [the creation example](examples/CREATE-A-UNIVERSE.md).
- **Registry:** a service for retaining and distributing versioned reusable
  artifacts. For a universe, image digests remain linked to its composition and
  qualification records. Recommended once verified realizations are worth
  duplicating; not required for first construction. See the
  [reference procedure](procedures/01-REFERENCE-UNIVERSE.md#registry-after-verification).

## Work and evidence

- **Receipt / acknowledgment:** evidence of a specifically declared acceptance or
  transition, not automatically of the intended final effect. See
  [units](learning/04-UNITS-AND-DEPENDENCIES.md).
- **Lease:** a bounded, time-limited claim to work under a contract. Expiry does
  not prove that the previous worker produced no effect. See
  [C4](examples/COMPREHENSION-CHECKS.md).
- **Outbox:** pending evidence or delivery obligations persisted with the owning
  local state transition so they can be reconciled and delivered after failure.
  It is not itself proof that the recipient received them. See units.
- **Vault [TARGET S07]:** secret protection and authorized delivery, not business
  scheduling or general authorization. See units and the September profile.
- **Logger [TARGET S07]:** authenticated event evidence, ordering and integrity,
  not an oracle proving business truth. See units.
- **Queue [TARGET S07]:** durable deferred-work responsibility and leasing,
  not execution or result-quality judgment. See units.
- **Maestro [TARGET S07]:** due occurrences from declared schedules, not a general
  orchestrator; no schedule means no fabricated work. See units.
- **Cognition Bridge [TARGET S07]:** optional bounded cognition adapter, not a
  base dependency or an inter-universe business-data gateway. See units.

For package/brick/unit lineage, read the
[vocabulary boundary](architecture/VOCABULARY-BOUNDARY.md). No obligatory
“packages then bricks” conceptual sequence is inferred from the user's wording.

## Cognition and continuity

- **Jurisdiction:** the scope of responsibility and permitted action assigned by
  the human; a tool credential or shared host does not enlarge it.
- **Context package:** the relevant universe, mission, role, resources,
  relationships, rules, current state, prior actions and expected evidence,
  identified by revision and prepared by the tandem.
- **Logical session:** the stable work context identified by SHAPER, mapped to a
  provider session or explicitly reconstructed conversation.
- **Native session:** a provider-owned conversation identifier and state; it may
  disappear or lose relevant context independently of SHAPER's records.
- **Rehydration:** reloading authoritative current context and action/check
  records before continuing work; not an assumption of perfect model memory.
- **Action record:** durable operational history of intended, pending, completed
  and uncertain effects and their checks, owned by the responsible Runtime unit.
  It is distinct from a conversation transcript.
- **Operation versus run:** one business operation keeps its identity across
  retries; each bridge attempt has its own run identity.
- **Adapter capability:** behavior actually supplied and qualified by a concrete
  bridge, including context delivery, tools, execution policy and recovery.

These meanings are explained in the [generic bridge intent](intents/cognition-bridge.md).
