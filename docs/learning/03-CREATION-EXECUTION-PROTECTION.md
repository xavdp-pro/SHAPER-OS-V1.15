# 3. Creation, execution and protection

Status: teaching of the 22 September design direction; terminology is not yet
reconciled into successor law. Prerequisite: [layers and scopes](02-LAYERS-AND-SCOPES.md).
Sources: S05 and S07 in the [source map](../../review/SOURCE-MAP.md).

## In plain language

Describe what should exist, what lets it run, and what controls its interactions.
These are three questions about the same system, not three new products to buy.

**[TARGET S05: The four terms; S07: Terms, explanatory versus binding]** The
framework vocabulary below is preserved design input pending canonical mapping.
The price-import illustration is explanatory, not an adopted business policy.

## What is it?

The Creation Framework describes the intended function, composition, limits and
required proof before an instance exists. It survives replacement of the instance.
The Execution Framework describes how the instance is hosted and constrained.
The Protection Framework describes controlled permeability: identities, roles,
permitted exchanges, refusals, evidence, containment and recovery.

These are complementary concerns, not three new products, servers or compulsory
deployment stages. Protection shapes creation and execution from the beginning.
The functional unit is what carries a bounded responsibility; it is not a fourth
framework with the same meaning as the other three.

## Why does it exist?

Specifying only a service's useful behavior leaves unanswered who may invoke it,
what it depends on, how it stops and how its state survives. Separating the three
questions makes these omissions visible without binding the OS to one technology.

## In practice

For a price-import unit, creation specifies accepted supplier inputs, effective
dates, preservation of old quotations and acceptance evidence. Execution declares
the operational identity, resource needs, dependencies, persistent state and
lifecycle. Protection declares permitted callers, allowed fields, refusal on
revocation, controlled data crossings and recovery authority.

A container is one execution choice. An authorization mechanism realizes part
of protection; it does not replace its policy. An attractive “capsule” drawing
is an explanatory boundary, not proof of isolation.

## What can fail?

Creation disappears into implementation details; protection is added after all
interfaces are exposed; restarting invents a new identity or empty database;
or ordinary application credentials acquire administrative power. A functioning
instance can still violate its intended boundaries.

## How do we verify understanding?

Explain how to replace an implementation while retaining its meaning, identity
continuity, owned state and proofs. Identify what comes from creation, what must
be provided by execution and what protection forbids. Then explain the refused
case, not just the successful call. Detailed unit contracts remain required.

Next: [units and dependencies](04-UNITS-AND-DEPENDENCIES.md).
