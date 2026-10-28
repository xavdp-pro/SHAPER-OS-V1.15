# Working glossary

Purpose: explain the vocabulary used to understand and apply SHAPER OS.
Canonical concept IDs and meanings belong to the [independent glossary](https://github.com/xavdp-pro/shaper-glossary/blob/main/TERMS.md).
This page explains their SHAPER OS use under the [source-role contract](architecture/SOURCE-ROLES.md); historical attribution remains in the local [source map](../review/SOURCE-MAP.md).
Definitions are **EXPLANATION**, except terms explicitly labeled **TARGET**.
Technical and client terms follow the [27 October vocabulary direction](../decisions/2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md):
agent-facing pages lead with the technical term, human-facing pages with the client term.

## Discernment and delivery

- **Agentic overzealousness:** assurance work that perpetuates itself while
  delaying the useful result it should support.
- **Progressive satisfaction:** the human's gradual, revisable appreciation of
  coherence and usefulness through using an assembled system.
- **Apparent usability:** a provisional judgment grounded in interactions
  actually tried, not a claim of complete qualification.
- **Current level of exigence:** what must work for the thing being built and its
  present use, under the human mandate and applicable obligations.

Read [Prevention of Agentic Overzealousness](human/PREVENTION-OF-AGENTIC-OVERZEALOUSNESS.md)
for human context, agent decisions, examples and limits.

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
- **Adopted editorial foundation:** the guidance for reading, explaining and
  maintaining the framework, with its owners identified in the
  [governing corpus](GOVERNING-CORPUS.md#authority-and-ownership).
  Distinguish this guidance from the operational laws and unit contracts;
  neither a reading summary nor an example replaces or waives them.
- **Finite study set:** the larger enumerated reading set in that map, including
  explanatory chapters, examples and reviews; inclusion does not confer law status.
- **Complete rulebook:** the [root index and seven canonical rule files](../RULES.md#complete-rulebook).
  The index locates each rule; the linked owner contains its full binding text.
  Dividing files does not divide authority or make any rule optional.
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
- **Universe (client term: space):** the logical sum of the cells of one
  organization, enterprise, shop or project, declared by membership in its
  governor's records. It has no physical envelope and is distinct from a
  filesystem folder, container, host or access grant. Earlier sources used
  “universe” for one operational composition and described a space containing
  universes; read those uses by the
  [vocabulary direction](../decisions/2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md#reading-earlier-sources).
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
- **Process / binary (level 0):** executable material beneath a functional unit;
  engineering detail, outside client vocabulary.
- **Functional unit (FUnit, organelle; client term: component):** a bounded
  responsibility with identity, owned state, declared contracts, lifecycle and
  proof obligations. “Brick/brique” remains a compatibility alias; `brick-*`
  names remain stable artifact identifiers.
- **Cell:** a composition of functional units with its own boundary and
  contracts. The **generic stem cell** is the reusable base cell; a **specialized
  cell (client term: service)** is that base plus one or more domain functional
  units, for a business, support or transversal purpose.
- **Supervision cell (client term: cockpit):** a cell that reads the state of
  several universes by pull or published events, outside their transactional
  paths; its failure never stops a universe.
- **Governor (public root cell; client term: guichet, its request interface):**
  owns approved desired state and receives requests; it holds no host power.
- **Maker (private root cell; client term: fabrication workshop):** claims
  approved work, applies frozen recipes that instantiate and specialize cells,
  and attaches them to a universe. A root cell is not root authority.
- **Class / specialization / instance:** reusable versioned definition, declared
  derivation, and one stable owned materialization respectively. See [composition](architecture/COMPOSITION.md).
- **Lifecycle level (K, K+1, N):** a level of the tree that says who repairs,
  updates, creates and ends whom. An instance's parent level is its governor and
  the makers that governor enrolled; the maker alone holds host capability. It is
  not a composition level 0–4: universes never contain universes. See the
  [28 October rules and contracts direction](../decisions/2026-10-28-RULES-AND-CONTRACTS-VOCABULARY.md).

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
  artifacts. For a cell, image digests remain linked to its composition and
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
“packages then components” conceptual sequence is inferred from the user's wording.

## Cognition and continuity

- **Jurisdiction:** the scope of responsibility and permitted action assigned by
  the human: universes, or some cells within them. A tool credential, a shared host or
  universe membership does not enlarge it.
- **Context package:** the relevant universe and cell, mission, role, resources,
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
