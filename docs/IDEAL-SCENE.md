# SHAPER OS in practice — the ideal scene

Purpose: **EXPLANATION** of the reference architecture and intended experience,
following the [2 October presentation decision](../decisions/2026-10-02-PRACTICAL-USE-AND-REFERENCE-SCENE.md).
SHAPER OS V1.15 is ready for use and is used daily to organize and deploy
universes. This scene helps you
understand and try its method; concrete capabilities belong to the realization
and version you choose.

## Begin with the human need

You want tools that fit your organization and can evolve with it. You explain
what matters, which results you want, what must be preserved and where agents
may take initiative. SHAPER OS gives the human and agents a shared frame for
turning that intention into a system, checking its effects and improving it.

The human remains in command. Shared responsibilities and ethical principles support
initiative, improvisation and invention in how the work is achieved.

## An adaptable space of universes

An entity's **space** brings together its **universes**, each with a purpose,
identity, owned state and declared exchanges. One organization may choose a
telephony universe, another an enterprise universe, and another both. Their
composition and relationships adapt to the activity.

**Helm** lets the human pilot the universes within their jurisdiction: act on
them, shape their behavior and follow their work. Helm is not the container that
holds the other universes. The space contains them; the jurisdiction defines
the perimeter of responsibility and permitted action.

A universe contains **functional units**, each responsible for a bounded function
and its state. Under the current Podman/MariaDB construction model, each unit has
its own runtime container and private MariaDB. See the
[scoped profile](profiles/SEPTEMBER-CONTAINER-MARIADB.md).

## From a request to a universe

Consider a service offering a personalized space to a client. A validated order
requests a new universe under the agreed service conditions. A **governor**
coordinates the creation work; one or more **makers** carry it out within their
mandates and report the result. Helm lets the client pilot the resulting universe
within their jurisdiction.

Makers can operate on the selected infrastructure. In a container realization,
**PodMesh** supplies the container-management foundation; its own contracts and
version describe placement, migration and recovery behavior. A governor, maker
and PodMesh manager have different responsibilities.

The same pattern can recur at different scales: intention, scope, coordinated
work, observation and correction. That is the fractal idea. Each scope retains
its own responsibilities and declared relationships. The pattern adapts to each
situation, allowing different compositions and physical arrangements.

## Try the framework with an agent

Begin with a focused case: for example, update future quotations from a supplier's
new prices while preserving previously accepted quotations.

1. Give your agent the repository and ask it to follow the
   [reading board](CONTEXT-INDEX.md) and [agent entrance](../AGENTS.md).
2. Describe the desired result, affected scope and what must remain unchanged.
3. Ask the agent to explain the intention, state owners, dependencies, allowed
   actions, recovery needs and observations that would establish success.
4. Compare that explanation with your own intention. Ask for another perspective
   on assumptions or omissions; correct the plan before performing effects.
5. If you choose implementation, use a separate realization repository with its
   applicable governing revision and an explicit mandate. Start with a focused
   exercise, inspect the actual result and retain the lessons.

You can begin by asking:

> Read SHAPER OS through its agent entrance. Help me express my intention and
> explore ways to make it real. Explain the responsibilities, relationships,
> state and recovery, and how we will observe the result. Bring your ideas,
> identify what needs clarification and propose a first useful step within
> our agreed scope. Help me improve the plan as we learn from practice.

The first useful result is a shared, inspectable plan. Reading this repository
requires no particular model provider or hosting service. Implementation uses
its own tools, contracts and operating conditions.

## Go further

- [Create a universe with an agent](examples/CREATE-A-UNIVERSE.md): a concrete
  request naming the destination, purpose and hosting choice, with Proxmox/LXC
  as one example.
- [Human reading guide](human/READING-GUIDE.md): choose your depth of explanation.
- [Shared learning sequence](CONTEXT-INDEX.md#common-learning-sequence): connect
  intention, architecture, functional units, realization and learning.
- [Reference universe procedure](procedures/01-REFERENCE-UNIVERSE.md): derive a
  concrete base under a declared construction profile.
- [SHAPER Three Layers](https://github.com/xavdp-pro/shaper-three-layers): OS,
  Runtime and Workspace perspectives.
- [PodMesh](https://github.com/xavdp-pro/podmesh): the separate container realization.

For editorial reconciliation, consult the [ledger](../review/READING-LEDGER.md).
For a concrete deployment, consult that realization's versioned records.
