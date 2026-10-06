# Vocabulary across intention and realization

Purpose: connect functional responsibility, reusable code and deployable
artifacts, so readers can move clearly from intention to realization.

## Current definitions

A **package** is reusable implementation material without an independent
runtime lifecycle. A **brick** is a deployable artifact with one declared
responsibility. A **functional unit** is defined by its purpose, bounded
responsibility, identity, private state, lifecycle and observable proof.
The current container profile realizes each unit in an isolated Podman container
with private MariaDB. These obligations are carried in the local
[rules](../../RULES.md), [naming contract](NAMING.md) and
[container profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md).

## Distinction used in V1.15

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

## Local owners

- [Naming and artifact vocabulary](NAMING.md).
- [Functional-unit rules](../../RULES.md).
- [Container and MariaDB profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md).
- [Code-free framework direction](../../decisions/2026-09-23-AGNOSTIC-NO-CODE.md).

The applicable contracts define the obligation; the realization records its
concrete composition and observed results. No historical repository is needed
to understand these distinctions.
