# 4. Functional units and explicit relationships

Purpose: explain functional units and their relationships, with the September
construction profile as a concrete example.
Prerequisite: [frameworks](03-CREATION-EXECUTION-PROTECTION.md).
Sources: S02, S05 and S07 in the [source map](../../review/SOURCE-MAP.md).

## In plain language

Give each part a clear job and state exactly what it promises to other parts.
Accepting a request, recording an event and doing the actual work are different
jobs; one success must not be mistaken for another.

**[EXPLANATION S05]** The general
unit explanation below does not extend the target profile to every technology.

## What is it?

A functional unit owns one bounded responsibility, identity, state, lifecycle
and observable proof. Its relationships explain what it needs and promises.
Its [brick and implementation package](../architecture/VOCABULARY-BOUNDARY.md)
are realization concerns, not synonyms for its meaning.

For every relationship identify producer and consumer, purpose, authority,
accepted inputs, outputs, compatibility, persistence, startup needs, refusal,
timeouts, retry and duplicate handling, evidence and recovery. Distinguish a
build-time dependency from a running service dependency.

## Why does it exist?

A list of components cannot explain behavior after a partial failure. Explicit
contracts prevent two units from both assuming the other owns an obligation, or
neither owning it. An acknowledgment must say precisely what it acknowledges.

## In practice: the September target

**[TARGET S07]** Four base responsibilities are mandatory
in the [September target profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md),
per minimal universe composition, not universally for every possible profile:

- Vault (P1) protects secrets and delivers them to authorized unit incarnations.
- Logger (P1) records authenticated events and proves their ordering and integrity.
- Generic Queue (P1) holds deferred work durably and leases it until terminal acknowledgment.
- Maestro (P2) determines when declared recurring work is due and submits an
  idempotent occurrence. With no schedule it creates no work.

“Base” describes this required composition, while P1/P2 describe each unit’s
[architectural perimeter](../architecture/PERIMETERS.md). A deterministic scheduler
can belong to P2 and remain independent of cognition.

A responsible consumer performs the requested effect. A Cognition Bridge is
optional when a declared job needs cognition; base units do not depend on it.
It is not the general inter-universe data gateway. A door in the Protection
Framework defines those exchanges.

**[MANDATE: 24 September reference choice]** The selected
[reference-universe composition](../procedures/01-REFERENCE-UNIVERSE.md)
includes an OpenCode bridge by default. It adds a fifth unit to that reference,
without making the four base responsibilities depend on cognition.

Maestro submits to Queue; Queue's consumer performs the effect; state-owning
units preserve evidence for Logger. Vault supplies scoped runtime identities.
These sentences describe distinct exchanges, not a single total startup order.
The detailed bootstrap must avoid circular dependencies, including Vault's
initial identity and key continuity. Those are supplied by its declared parent
construction path, not invented by an already running Vault.

## Scope placement

**[TARGET S05]** The profile places the units
inside the Execution Framework of one running universe. Its base Logger owns
that universe's declared evidence responsibility; one shared Logger must not
silently replace two universes' separate units. Any permitted aggregation is a
distinct function and data crossing with its own contract.

**[EXPLANATION]** The realization declares its space-level composition, actual
door-ratification roles and nesting limits under the local perimeter and topology
contracts. Resolve a business-specific choice with the authorized owner when needed. Fractal
composition uses explicit local authority, resource limits and unit responsibilities.

## What can fail?

Queue's acceptance is mistaken for completed work; Logger's receipt is mistaken
for proof that a business effect happened; Maestro becomes a general orchestrator;
or Bridge is made a mandatory source of authority. A dependency failure must
produce a declared unavailable/degraded state, not fabricated success.

**[TARGET S07]** Within this profile,
each functional unit has its own MariaDB and identity, with an
unprivileged application account. State transitions and pending evidence are
recorded together locally; cross-unit atomic transactions are not assumed. Active
obligations are not expired into history merely because a calendar period ends.
These concrete target obligations remain intact; the
[profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md) fixes the applicability
boundary. Read the local [rules](../../RULES.md) and detailed
[unit contracts](../GOVERNING-CORPUS.md) for the complete obligations.

## How do we verify understanding?

**[EXPLANATION]** This is a conceptual test, not profile selection or deployment.

Explain a worker failure after a committed effect but before acknowledgment.
Who owns the effect, deduplication, lease, retry and evidence? Then explain why
the absence of a cognition provider cannot disable the four base responsibilities.
Read the detailed local Queue, Logger and lifecycle contracts before answering.
If a requested business behavior has not been specified or tested, record that
precise gap instead of claiming an end-to-end proof.

Next: [from contracts to materialization](05-MATERIALIZATION.md).
