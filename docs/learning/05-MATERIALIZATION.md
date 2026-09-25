# 5. From generic intention to concrete realization

Status: candidate interpretation of the explicit code-free mandate. The precise
scope of inherited technology requirements remains a reconciliation item.
Prerequisite: [units and dependencies](04-UNITS-AND-DEPENDENCIES.md).
Sources: S01, S02, S03, S04, S05 and S07 in the [source map](../../review/SOURCE-MAP.md).

## In plain language

Keep what the system must mean separate from the code that makes it work today.
A better implementation is welcome only if it preserves commitments and data,
and proves the required behavior again.

**[MANDATE: 23 September 2026]** Implementation stays outside SHAPER OS. The remaining
teaching prose is **[EXPLANATION S03: Runtime master sections 19–20 and 24–31]**,
except the explicitly labeled September target below.

## What is it?

Materialization makes an intention operational under an explicit realization
profile. The OS explains purpose, responsibilities, constraints, relationships
and evidence. A separate realization repository owns implementation packages,
brick artifacts, executable schemas, migrations, manifests, tests and deployment
recipes. No implementation language or database engine is necessary to read OS.

## Why does it exist?

Today's implementation is not the ceiling of tomorrow's agents. The human wants
better implementations possible in one, three and six months without losing the
meaning of work already entrusted to the system. This is a design motivation,
not a promise about future model performance.

Agnostic does not mean vague or interchangeable without proof. The replacement
must satisfy the contract, preserve historical meaning and safely migrate owned
state. A changed principle also requires explicit human-governed revision; it
cannot be smuggled in as an implementation improvement.

## In practice

The tandem agrees that future quotes use validated current prices while accepted
quotes retain their committed values. It selects a concrete profile, derives unit
contracts and dependencies, implements outside OS, verifies behavior, qualifies
deployment and records observed results. Packages may supply reusable code to
bricks; that is an implementation arrangement, not a replacement of “briques.”

**[TARGET S05/S07]** The [September profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md)
preserves the Podman/container construction model and private MariaDB per unit.
Creating another unit or universe under that model retains its obligations.
An agent cannot choose an alternate engine because the OS is agnostic. A future
profile requires explicit approval and an obligation-by-obligation mapping;
none is adopted here. The successor's generic-law mapping remains F-02/F-05.

## What can fail?

**[EXPLANATION S03: Runtime master sections 19–20 and 24–27]** These general
failure distinctions are not confined to the September target.

“Generic” removes all detail; “better code” overwrites production data; a new model
receives more authority by default; or an example quietly becomes universal law.
A regenerated image is not a regenerated business history. Before irreversible
effects, define compensation or reconciliation rather than promising impossible
rollback, such as unsending an already delivered message.

## How do we verify understanding?

**[EXPLANATION S03: Runtime master sections 24–31]** These are general realization
obligations to explain and reconcile, not a claim that the September profile is
the only possible implementation.

Before declaring a realization deployable, locate its versioned composition,
identity/bootstrap contract, prerequisites, state ownership, permissions,
startup/readiness conditions, failure behavior, backup and proven restoration,
migration/canary plan, operating limits, observable effects and handoff owner.
These are documentation obligations here; their executable forms live elsewhere.

Explain which of those must be re-qualified when only code changes, and which
when storage or hosting changes. “Same API” is insufficient evidence that data,
timing, security and recovery semantics remain the same.

Next: [evidence, recovery and learning](06-EVIDENCE-RECOVERY-LEARNING.md).
