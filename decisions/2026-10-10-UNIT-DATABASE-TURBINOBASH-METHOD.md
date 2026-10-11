# Operator direction — the unit database follows the Turbinobash method

Direction: **[MANDATE]** scoped operator direction of 10 October 2026, for the
[September container and MariaDB target](../docs/profiles/SEPTEMBER-CONTAINER-MARIADB.md).
Status: the operator's request is recorded below. The provisions it adds to
local [Rule 4](../docs/rules/02-CONSTRUCTION.md#rule-4) and
[Rule 26](../docs/rules/05-REPAIR-AND-DATA.md#rule-26) bind from the revision
the operator explicitly adopts. It completes the
[24 September functional-unit MariaDB direction](2026-09-24-FUNCTIONAL-UNIT-MARIADB.md),
certifies no built image or universe, and grants no exception.

## Provenance

Source: operator direction issued on 10 October 2026. The operator stated that
the private MariaDB of a functional unit is "like Turbinobash, carried over to a
single user", asked that the method be written out — one system user, one
database user, the database named like the application, the password in `etc` —
and that it be remembered as the rule to apply whenever an application is built.

Turbinobash is the origin of the method, not a reference realization. The
inspected application-creation path selects grants with the grant option; the
inspected credential and ownership paths also use command-line passwords and
recursive ownership changes. These implementation choices are not inherited.

## Why it is written now

Facts found on 10 October 2026, bounded to the sources and revisions inspected:

- The per-functional-Podman convention entered the V1.14 rules on
  22 September 2026 (SHAPER-OS-V1.14 commit `883343e`). Before it, Rule 4 read
  "On-Demand Database Isolation" and Rule 26 "MariaDB per Universe". A universe
  inspected on 10 October had been built earlier, under that previous rule. On
  the V1.14 main line examined (`958e0b7`), the Vault, Logger, Queue and Maestro
  bricks had not been converted since.
- A conversion of the four base units placed each MariaDB in a separate
  container beside its application. The words "inside that Podman's security and
  lifecycle boundary" allowed that reading.
- The existing profile already requires the four base units and permits an idle
  Maestro. This direction makes their qualification and implementation
  obligations explicit.

## What it settles

1. **The method.** Rule 4 spells out the Turbinobash method, one application
   account per server: one declared functional identity for the application's
   Linux account, MariaDB account and database; the MariaDB server in the same
   container as the application, on a private socket only; the password file
   in `/apps/<functional-slug>/etc/mysql/localhost/passwd`; root administering
   through its own path; a recovery point that includes the database dump.
   Rule 26 adds the inventory that qualification performs, so that a separate
   database container, an empty database beside file-based state, or an
   unchecked entrypoint cannot pass.
2. **Base units.** Vault, Logger, Queue and Maestro are the universe's common
   services: secrets, append-only audit, deferred jobs and cadence. A mandatory
   base unit may remain operationally idle after passing its applicable
   functional, isolation, persistence and recovery qualification. No recurring
   artificial workload is required merely to keep it busy, and idle operation
   does not waive the finite qualification tasks required by the proof and unit
   contracts. A base unit does not conform when it is absent, disabled, or uses
   file stores instead of the required authoritative MariaDB state. A
   composition with no cognition requirement need not select a bridge; this
   does not alter the separately declared reference composition.
3. **Where corrections live.** Where a realization consumes a maintained
   catalogue, corrections belong in its reusable bricks and supported birth
   recipes, with their qualification evidence. When no suitable qualified
   artefact exists, the constructor builds and qualifies one from the governing
   contracts; first construction requires no pre-existing catalogue or registry.
   A convention change identifies the affected implementations, recipes and
   consumers, with an owning correction work item. A candidate with an unmet
   birth gate remains unqualified; recording a gap does not authorize takeover
   or promotion.

## Amendment, 11 October 2026 — who owns the home

A container proof on a disposable host showed that an application account owning
`/apps/<functional-slug>/` can rename `sav/` and so replace its own database directory, which
point 2 of the method forbids. The operator decided that the home stays the account's home but is
owned by root; the account owns only what it writes (its password file and its declared
application data paths). Rule 4 point 1 says so.

## What it does not do

Existing deployed universes do not change by this document. Their governing
revisions and actual stores remain separate evidence, and a recorded gap is not
compliance.
