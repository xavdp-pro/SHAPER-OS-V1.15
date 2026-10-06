# September container and MariaDB target

Profile identifier: **SEP22-CONTAINER-MARIADB**.
Purpose: describe the Podman and private-MariaDB construction profile, including
unit ownership, composition, bootstrap and recovery. **TARGET** statements
apply within the declared profile; realization records describe actual operation.
Owners: local [RULES](../../RULES.md), [topology](../architecture/TOPOLOGY.md),
[unit contracts](../GOVERNING-CORPUS.md) and the scoped decisions below.
The [source map](../../review/SOURCE-MAP.md) connects their local meanings.

## Applicability

**[TARGET S05/S07]** This is the preserved target for reconstruction of the
functional units in the existing SHAPER universe construction model described
by those sources. “Existing work” means work governed by that model, not merely
files created before a calendar date. Creating a new unit or a second universe
under the same model does not exempt it from these obligations.

**[EDITORIAL]** This edition records the selected construction profile. Its
applicable obligations guide realization choices. For a new operational request, record the governing
realization and whether its declared construction model adopts this target.
If scope is uncertain, resolve it with the authorized owner before selecting a
conflicting storage or isolation mechanism. No alternate profile is adopted here.

A “future profile” means a separately proposed, explicitly approved construction
model with a documented mapping of all affected obligations and new qualification.
It is not a choice an implementation agent may infer from the word agnostic.
For new work under the current construction model, the owner has answered the
applicability question: see the
[24 September functional-unit MariaDB decision](../../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md).
The local [rules](../../RULES.md), [topology](../architecture/TOPOLOGY.md)
and [perimeters](../architecture/PERIMETERS.md) carry these obligations in
this edition. See the [governing corpus](../GOVERNING-CORPUS.md) for their owners.

## Practical topology

**[MANDATE: 6 October clarification]** The operator reports repeated deployment
and extensive daily use of this universe model, including nested Podman.
Podman hosting retains an outer system-container universe running its inner
Podman functional units; LXC hosting supplies that outer system boundary.
An isolated host application network does not replace the universe container.
Each unit has its own MariaDB server instance, not merely a separate database
on a shared server. Docker and a shared development database are not adopted
alternatives here.

The [current construction crosswalk](../GOVERNING-CORPUS.md#current-construction-crosswalk)
identifies the current local requirements. Qualify the newly generated candidate
and chosen host while preserving the operator-attested record of practical use.

## Preserved choices

**[TARGET S05/S07]** Each functional unit has one responsibility, one isolated
runtime container in the Podman realization, its own system identity and its own
private MariaDB. Its functional slug identifies the unit, system account,
database account and database. Application permissions are limited to that
database; administration uses a separate authorized path.

In each minimal universe composition, Vault, Logger, Queue and Maestro are the
four mandatory base units. Under the [perimeter taxonomy](../architecture/PERIMETERS.md),
Vault, Logger and generic Queue are P1; Maestro is P2. “Base” names the composition,
not a single perimeter. Cognition Bridge is optional when a class declares
bounded cognition jobs (see the
[generic bridge intent](../intents/cognition-bridge.md) and its scoped adapters). No base unit depends on that adapter. Maestro remains
idle when no schedule is declared. This is a property of **this target**, not a
claim that every imaginable implementation must contain these four products.

**[MANDATE: 24 September reference choice]** The
[operator decision](../../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md)
and [Reference Universe Procedure](../procedures/01-REFERENCE-UNIVERSE.md) now
select the [OpenCode Cognition Bridge](../intents/cognition-bridge-opencode.md)
by default as a fifth unit in that
reference composition. The four base responsibilities above remain independent
of the bridge; an installed bridge may remain idle until authorized work is
declared. This scoped choice does not turn OpenCode into a universal
technology law or assert that a new reference has already been built.

Each unit preserves a durable evidence outbox together with its state transition.
Logger's receipt, Queue's responsibility and the consumer's real effect have
different meanings. No cross-database atomic transaction is assumed. Active
obligations do not become settled history because a month ended.

## Scope placement and unresolved structure

**[TARGET S05/S07]** The Execution Framework describes and constrains the hosting
of the units of one running
universe instance. Each minimal universe has its declared base composition;
the sources do not authorize replacing two universes' Logger units with one
shared state-owning Logger merely because they share a space or host. A separate
aggregation view would be a different declared function and crossing, not an
implicit merge of their authoritative histories.

**[OPEN F-03a]** The sources reviewed here do not specify a mandatory base-unit
composition for a containing space itself. Do not recursively manufacture one.
**[TARGET]** Use the local [perimeter contract](../architecture/PERIMETERS.md)
for doors across jurisdictions. The realization identifies its actual authority
roles and approval records. A sender's request or a UI declaration alone is not
proof of the receiving side's authorization.
**[OPEN F-03c]** Define permitted space nesting and recursion depth for the
chosen realization with the authorized owner. Its composition declares finite
scope, resource limits and authority before recursive creation. The editorial
crosswalk tracks the general mapping of these choices.

## Bootstrap and recovery direction

**[TARGET S07]** The parent construction path supplies initial Vault identity,
database access and separately delivered matching key material. Vault verifies
continuity before other units obtain scoped credentials. The reconstruction
direction is Vault, then Logger, Queue, Maestro, followed by optional Cognition
Bridge if selected. This is a dependency direction, not a substitute for each
unit's readiness, outbox, lease and failure contract.

Before data-bearing migration, prove restoration of the owning unit's database
and persistent volumes, then qualify a bounded rollout. Rebuilding an image must
not silently create an empty database or a new Vault cryptographic identity.

Read the detailed local [Vault](../contracts/vault.md),
[Logger](../contracts/logger.md), [Queue](../contracts/queue.md),
[Maestro](../contracts/maestro.md), [bridge](../intents/cognition-bridge.md)
and [lifecycle](../agent/LIFECYCLE.md) contracts before deriving startup,
recovery and acceptance tests. The realization defines and verifies its actual
coherent recovery points. This profile contains no executable configuration,
schema or implementation recipe.
