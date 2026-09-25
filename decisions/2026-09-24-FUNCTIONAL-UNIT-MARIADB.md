# Operator direction — a private MariaDB for every next functional unit

Status: **[MANDATE]** scoped operator direction issued on 24 September 2026. It
applies the preserved
[September container and MariaDB target](../docs/profiles/SEPTEMBER-CONTAINER-MARIADB.md);
it does not seal V1.15 as successor runtime law, make MariaDB a universal
requirement for every possible future realization, or certify a built image or
universe.

## Provenance

Source: operator direction issued on 24 September 2026. The public record below
states the direction in English. The operator asked for it to be noted "very
strongly": the next pieces of work, Vox or other, follow the functional-unit
standard as already specified, in which each functional Podman unit owns its
own MariaDB. The same day the operator also directed that one running development
instance keep its current SQLite storage for a walkthrough.

## Scope

- **Which work:** every new piece of work under the current SHAPER construction
  model, that is the Podman realization governed by V1.14 and preserved by
  profile SEP22-CONTAINER-MARIADB: new functional units, new universes, and new
  durable stores added to existing units, whatever the class (Vox or other).
- **What it settles:** the profile asks, for a new operational request, whether
  its construction model adopts this target, and sends uncertain scope to the
  authorized owner. The owner has answered for this work: it adopts the target.
  No agent re-decides that per request, and the profile already forbids an agent
  choosing it away.
- **What it cites, not replaces:** the profile's "Preserved choices" (one
  responsibility, one isolated runtime, its own identity and its own private
  MariaDB, the functional slug naming unit, account and database); V1.14
  `software/RULES.md` Rule 4, "Mandatory Functional-Podman Database Convention",
  including "Born With the Function"; and V1.14 Rule 26, "Complete Database
  Isolation (MariaDB per Functional Podman)".

## What an agent does

- A new durable store is created in the owning unit's private MariaDB, born with
  the unit. SQLite, CSV, JSONL or another engine is not chosen instead, and the
  word "agnostic" is not read as permission to do so.
- As in V1.14 Rule 4, SQLite, CSV and JSONL may exist only as declared,
  disposable development scaffolding. They never count as the unit's database,
  as evidence of conformity, or as a promotion gate.
- A work brief that stores anything says so explicitly, in the same way it
  states the English-in-repository boundary.

## Prototype debt stays separate

- Prototypes already running SQLite, JSON or CSV stores are declared development
  debt. That debt is not conformity evidence, not an exception, and not a
  precedent. It is not extended. Migration and restore tests are separate work
  items, with no silent change to a running instance.
- A temporary direction to leave one instance's storage unchanged, for example
  for a walkthrough, is operational scope for that occasion. It is not an
  exception to this direction.
- This record grants no exception.

Existing deployed universes do not change by this document; their governing
revisions and actual stores remain separate evidence.
