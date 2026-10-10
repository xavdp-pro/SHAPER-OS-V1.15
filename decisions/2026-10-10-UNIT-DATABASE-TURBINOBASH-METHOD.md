# Operator direction — the unit database follows the Turbinobash method

Direction: **[MANDATE]** scoped operator direction issued on 10 October 2026. It
clarifies local [Rule 4](../docs/rules/02-CONSTRUCTION.md#rule-4) for the
[September container and MariaDB target](../docs/profiles/SEPTEMBER-CONTAINER-MARIADB.md)
and completes the
[24 September functional-unit MariaDB direction](2026-09-24-FUNCTIONAL-UNIT-MARIADB.md).
It does not certify a built image or universe, and it grants no exception.

## Provenance

Source: operator direction issued on 10 October 2026. The operator stated that
the private MariaDB of a functional unit is "like Turbinobash, carried over to a
single user", and asked that the method be written out: one system user, one
database user, the database named like the application, the password in `etc`.

## Why it is written now

Three facts were found the same day:

- The per-functional-Podman convention entered the rules on 22 September 2026.
  Universes built before that date were built under the earlier rule, one MariaDB
  per universe, on demand. Their base units came from a brick catalogue whose
  base bricks were never converted on its main line, so no conforming base unit
  existed to start from.
- A conversion of the four base units placed each MariaDB in a separate
  container beside its application. The words "inside that Podman's security and
  lifecycle boundary" allowed that reading.
- Nothing said what a base unit must be in a business universe that does not
  use it yet.

## What it settles

1. **The method.** Rule 4 now spells out the Turbinobash method, one account per
   server: one system account named by the functional slug with its home in
   `/apps/<functional-slug>/`, the MariaDB server in the same container as the
   application, one MariaDB account and one database with the same name, the
   password in `/apps/<functional-slug>/etc/mysql/localhost/passwd`, root
   administering through its own path, one dump per unit. A separate database
   container is not this method.
2. **Base units.** Vault, Logger, Queue and Maestro are the universe's common
   services: secrets, append-only audit, deferred jobs and cadence. Every
   composition under this profile carries the four, each with its own database
   by this method, even when no business unit uses it yet. An idle base unit
   conforms when it is healthy, has its database and can perform its contract.
   It does not conform when it is absent, disabled or running on files. An idle
   Maestro simply has no scheduled task; no proof task is required to keep it
   busy. The cognition bridge stays optional and is omitted when no unit
   declares cognition jobs.
3. **Who supplies them.** The brick catalogue publishes conforming base units
   as immutable, qualified digests. A new universe is born from those digests;
   it does not convert base units on its own.
4. **When the convention tightens again.** A change to the database convention
   comes with a catalogue work item that brings the base bricks to it. Until
   those bricks are published, a new birth that needs them is blocked or
   declared as a gap, never presented as conforming. Running universes keep
   their recorded transition under Rule 26.

## What it does not do

Existing deployed universes do not change by this document. Their governing
revisions and actual stores remain separate evidence, and a recorded gap is not
compliance.
