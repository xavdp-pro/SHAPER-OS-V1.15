# Vocabulary across intention and realization

Status: explanatory reconciliation note, not a completed successor lexicon.

## What the existing definitions say

V1.14's artifact-boundary document distinguishes a **package**, reusable source
code without an independent deployment lifecycle, from a **brick**, a deployable
image/container with one declared responsibility. Its brick taxonomy also
contains older formulations whose relationship to the 22 September decisions
must be reconciled.

The 22 September design decision defines a **functional unit** by one purpose,
bounded responsibility, identity, private state, lifecycle and observable proof.
Its concrete target uses an isolated service container and private MariaDB.
Those concrete choices are not silently erased by V1.15's agnostic boundary.

## Working distinction for the V1.15 review

SHAPER OS describes the meaning of a function and the obligations of its
relationships. A realization chooses and documents how that function is built.
In the existing container realization, implementation packages can contribute
code to a deployable brick that realizes the functional-unit contract.

These are different questions: what responsibility is needed; what code is
reused; what artifact can be deployed; what is actually running? Do not assume a
one-to-one mapping between them without the realization's composition contract.

The three-layer Runtime master uses “package” in another sense: an initial
organizational/domain pack of objects, policies and workflows. Qualify this as
an organizational pack rather than merging it with an implementation package.
This overload is recorded in the [glossary](../GLOSSARY.md); no new compulsory
packages-to-bricks ordering is introduced.

## Example

The Queue responsibility is to hold and distribute deferred work durably under
declared authority. Its contract explains acceptance, ownership, retry, failure
and evidence. In a chosen realization, a package implements that logic and a
brick delivers it with the required runtime and private storage arrangements.
A future implementation can replace the package while preserving and proving
the contract. None of that implementation belongs in this SHAPER OS repository.

## Source locators

- V1.14 at `c88fd87`: `docs/architecture/ARTIFACT-BOUNDARY.md` and `BRICKS.md`.
- P2 design record: `operator-deliverables/SHAPER-FRAMES-AND-FUNCTIONAL-UNITS-DESIGN-DECISION-2026-09-22.md`.
- Current operator clarification: [23 September decision](../../decisions/2026-09-23-AGNOSTIC-NO-CODE.md).

Pending: confront the latest rules and all unit contracts before adopting the
final lexicon and the precise scope of the MariaDB/container realization.
