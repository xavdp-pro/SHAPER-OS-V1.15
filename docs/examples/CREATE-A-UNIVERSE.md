# Ask an agent to create a universe

Status: **EXPLANATION** — simple starting requests for a human–agent tandem.

## Start with one sentence

> Create a SHAPER OS universe called univ-example in a Debian 13 LXC container on
> [target machine].

Or, on a Proxmox host:

> Create a SHAPER OS universe called univ-demo in an LXC container on the
> Proxmox machine [target machine].

Or, using an available Podman environment:

> Create a SHAPER OS universe called univ-example using Podman on [target machine].

Or, on the local machine:

> Create a SHAPER OS universe called univ-example locally using Podman.

The human names the universe, destination and preferred environment. The agent
organizes the construction there. The human does not need to write a deployment
specification before starting the conversation.

## Add the functions you already have in mind

Use the [glossary](../GLOSSARY.md) to name what you want to create: a space,
universe, functional unit, intention, role or jurisdiction. Naming these parts
and their relationships makes the request clearer and gives the human and agent
a shared vocabulary for building together.

If the human already knows what the universe should do beyond its base units,
include those intentions in the request. Describe each additional functional
unit's purpose, expected behavior, data and interactions with the other units.
The agent helps clarify the intentions and realizes them as additional Podman
functional units, each with its own responsibility and private database under
the current construction profile.

For example, continue the creation request with:

> In addition to the base units, add a product-catalog unit that owns product
> descriptions and current prices, and a quotation unit that prepares quotations
> using that catalog. Accepted quotations must retain their agreed descriptions
> and prices when the catalog changes. Help me express these intentions and
> organize the units and their authorized exchanges before implementing them.

The intention explains the useful result and what must be preserved. It does
not need to prescribe the implementation code. The agent connects those
intentions to the base composition, identifies dependencies and state owners,
then builds and verifies the additional units within the agreed scope.

## What needs to be available

The hosting prerequisite is Podman or LXC, with the permissions and resources
needed to create the requested environment. LXC may be managed directly on a
Debian host or through Proxmox. For the Debian 13 example, Debian 13 is the
requested LXC guest system; the agent checks the host and guest separately.

On the local machine, the agent works directly through its authorized local
access; SSH is not required. For a remote machine, the agent needs authorized
SSH access to that destination.

**Remote-machine tip:** give the target machine a memorable SSH alias in
`~/.ssh/config` on the machine from which the agent will connect. The alias is
the `Host` name; associate it with the destination's `HostName`, login `User`
and, when needed, its `Port` and `IdentityFile`. For example, name your target
`lab-host`, verify that `ssh lab-host` connects to the intended machine, then
use `lab-host` in your request. This makes the destination explicit without
repeating its address and connection options. Keep private keys and credentials
outside this repository; the alias identifies a destination, not permission to
act on it.

The agent checks access, capacity, networking and the available runtime. It
uses an existing suitable Podman installation rather than replacing it with
Docker. If installation or host configuration is needed, it explains the
change and performs it within the human's mandate. Missing access or a material
choice becomes a focused question, rather than a long questionnaire upfront.

## What the agent organizes

The agent reads SHAPER OS through its [entrance](../../AGENTS.md) and
[reading board](../CONTEXT-INDEX.md), identifies the applicable realization and
governing revision, and follows the
[reference universe procedure](../procedures/01-REFERENCE-UNIVERSE.md).
It preserves existing workloads while creating the new environment, constructs
or reuses the appropriate verified reference, and gives the new universe its
own identity, credentials and persistent state. Implementation and operating
records belong in a separate realization workspace.

Proxmox and LXC are example hosting choices. The LXC container hosts the
universe's environment; it does not replace the functional units or their
isolation and storage contracts. Under the
[current construction profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md),
functional units run in their own Podman containers, each with its private
MariaDB. Check the selected host's ability to support that composition before
building it; do not silently change the profile to work around a hosting issue.

## What to ask for at completion

Ask the agent to show the universe's identity and location, its functional units
and their responsibilities, a real operation demonstrating the requested
purpose, and the recovery result. Keep source checks, installation, observed
operation and human acceptance distinguishable.

This request starts a human–agent construction process. It does not imply that
a prebuilt image or a complete automated deployment is supplied by this
documentation repository.

Continue with the [reference universe procedure](../procedures/01-REFERENCE-UNIVERSE.md)
and the [ideal scene](../IDEAL-SCENE.md).
