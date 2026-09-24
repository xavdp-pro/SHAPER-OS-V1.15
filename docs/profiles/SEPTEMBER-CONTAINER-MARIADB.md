# September container and MariaDB target

Profile identifier: **SEP22-CONTAINER-MARIADB**.
Status: preservation of operator design input, not a sealed generic law,
completed unit specification or installed qualification.
Sources: S05 “Functional Unit”, “Relationship with the current canon” and
“Current maturity”; S07 “Mandatory construction invariants”, “Bootstrap boundary”
and “Reconstruction order” in the [source map](../../review/SOURCE-MAP.md).

## Applicability

**[TARGET S05/S07]** This is the preserved target for reconstruction of the
functional units in the existing SHAPER universe construction model described
by those sources. “Existing work” means work governed by that model, not merely
files created before a calendar date. Creating a new unit or a second universe
under the same model does not exempt it from these obligations.

**[EDITORIAL]** The candidate records this target; it does not grant the agent
power to choose it away. For a new operational request, record the governing
realization and whether its declared construction model adopts this target.
If scope is uncertain, resolve it with the authorized owner before selecting a
conflicting storage or isolation mechanism. No alternate profile is adopted here.

A “future profile” means a separately proposed, explicitly approved construction
model with a documented mapping of all affected obligations and new qualification.
It is not a choice an implementation agent may infer from the word agnostic.
For new work under the current construction model, the owner has answered the
applicability question: see the
[24 September functional-unit MariaDB decision](../../decisions/2026-09-24-FUNCTIONAL-UNIT-MARIADB.md).
The exact generalization of this target into successor law remains F-02/F-05.
See [interim authority](../GOVERNING-CORPUS.md) for existing operational versions.

## Preserved choices

**[TARGET S05/S07]** Each functional unit has one responsibility, one isolated
runtime container in the Podman realization, its own system identity and its own
private MariaDB. Its functional slug identifies the unit, system account,
database account and database. Application permissions are limited to that
database; administration uses a separate authorized path.

In each minimal universe composition, Vault, Logger, Queue and Maestro are the
four mandatory base units. Cognition Bridge is optional when a class declares
bounded cognition jobs. No base unit depends on that adapter. Maestro remains
idle when no schedule is declared. This is a property of **this target**, not a
claim that every imaginable implementation must contain these four products.

**[MANDATE: 24 September reference choice]** The
[operator decision](../../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md)
and [Reference Universe Procedure](../procedures/01-REFERENCE-UNIVERSE.md) now
select the OpenCode Cognition Bridge by default as a fifth unit in that
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
**[OPEN F-03b]** Exact authority roles and approval records for ratifying doors
across two jurisdictions still require the governing contracts. A sender's request
or a UI declaration alone is not proof of the receiving side's authorization.
**[OPEN F-03c]** Permitted nesting of spaces and any maximum recursion depth are
not yet reconciled. No unbounded self-reproduction is implied. A realization must
declare finite scope, resource limits and authority before any recursive creation.

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

**[OPEN F-05]** Detailed startup and recovery contracts, coherent cross-unit
recovery points and each unit's acceptance tests remain to be reconciled. This
document intentionally contains no executable configuration, schema or recipe.
