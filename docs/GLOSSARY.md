# Working glossary

Status: explanatory vocabulary, not a completed amendment of V1.14 Rule 37.
Definitions follow the [source map](../review/SOURCE-MAP.md). A conflicting
source must be reconciled before these terms become a sealed successor lexicon.
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
  already completed effect. See governance, source S03 OS master section 5.
- **Principal agent:** the agent coordinating understanding with the human and
  connecting affected contracts; a responsibility, not an automatic root identity.
  See the [agent routes](agent/STRONG.md).
- **Adopted candidate editorial foundation:** the five editorial documents
  enumerated in the [governing corpus](GOVERNING-CORPUS.md), not all operational law.
- **Finite study set:** the larger enumerated reading set in that map, including
  explanatory chapters, examples and reviews; inclusion does not confer law status.
- **Proof:** evidence sufficient for a specific claim under declared conditions,
  not a claim of absolute certainty or of unrelated capabilities.
- **Metacognition:** examining how one forms judgments and chooses actions.
- **Meta-regulation:** examining and improving the sensors, review and correction
  mechanisms themselves through authorized change.

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
  and the profile's open question F-03b about exact ratification roles.

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
  without its own independent deployment lifecycle in V1.14's definition.
- **Organizational pack:** an initial domain composition of concepts, workflows
  and policies. Some older Runtime documents also call this a package. Always
  qualify which sense is intended; do not equate it to an implementation package.
- **Realization profile:** an explicitly scoped set of concrete technology and
  deployment choices satisfying the generic contracts; not a loophole for
  weakening them. See [materialization](learning/05-MATERIALIZATION.md).
- **Realization repository:** the separately governed home of concrete code,
  executable artifacts, deployment recipes and their tests. Linking its obligations
  here does not import its implementation into OS. See materialization.

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
