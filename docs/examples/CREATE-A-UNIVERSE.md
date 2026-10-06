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

**The agent creates the implementation from SHAPER OS.** It can start with an
empty realization workspace: it writes the unit code, concrete contracts, build
material and tests there, outside this documentation repository. An existing
codebase, prebuilt reference or registry is optional reuse, not an entry ticket.

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

The hosting prerequisite is **Podman or LXC**, with the permissions and resources
needed to create the requested environment. LXC may be managed directly on a
Debian host or through Proxmox. For the Debian 13 example, Debian 13 is the
requested LXC guest system; the agent checks the host and guest separately.

| Available to start | What the agent checks or prepares |
| :--- | :--- |
| A capable coding agent with this repository and authorized tools | Read the frame, create files, run commands, build and observe results. Prior SHAPER history is unnecessary. |
| The named local machine or an SSH destination, with creation rights | Confirm the target, existing workloads, available CPU, memory, storage and network access. |
| Suitable Podman or LXC hosting | Prove that the chosen outer universe environment can run its inner Podman functional units; an installed binary alone is insufficient. |
| A separate writable realization workspace | Generate and retain code, tests, versioned composition and evidence. Prepare build dependencies from available sources within the mandate. |

Any credentials or external services needed by the requested functions are
checked before those functions are exercised. The default OpenCode bridge needs
a usable, authorized cognition engine for a real cognition test; the agent
implements its [adapter contract](../intents/cognition-bridge-opencode.md) and
[common continuity/execution intent](../intents/cognition-bridge.md). Missing engine
access is a precise dependency to resolve; the four base responsibilities remain
independent of cognition. The agent reports their results separately.

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
[reading board](../CONTEXT-INDEX.md), records the new realization's applicable
governing sources and profile, and follows the
[reference universe procedure](../procedures/01-REFERENCE-UNIVERSE.md).
It preserves existing workloads while creating the new environment, constructs
and verifies the first reference, or reuses a suitable verified one when available.
It gives the new universe its
own identity, credentials and persistent state. Implementation and operating
records belong in a separate realization workspace.

For these starter requests, use the reference composition selected by
Procedure 01: Vault, Logger, Queue, Maestro and the OpenCode bridge. This makes
the starting composition explicit; it does not make that adapter mandatory for
every possible profile. Report missing engine access separately from the
construction and operation of the four base units.

Proxmox and LXC are example hosting choices. The LXC container hosts the
universe's environment; it does not replace the functional units or their
isolation and storage contracts. Under the
[current construction profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md),
functional units run in their own Podman containers, each with its private
MariaDB. Check the selected host's ability to support that composition before
building it; do not silently change the profile to work around a hosting issue.

With Podman hosting under the current model, the universe is an outer system
container carrying its own Podman functional units. With LXC hosting, the LXC
guest supplies that outer boundary. The agent checks the nesting, storage,
network and privilege requirements on the actual host before claiming it is fit.
The operator reports repeated deployment and daily use of this nested model;
those practical results and qualification of the new candidate have their own
evidence scopes, as the [crosswalk](../GOVERNING-CORPUS.md#current-construction-crosswalk) explains.

Reuse the mandate, hosting choice and parameters already supplied. A Podman
hosting request follows the nested form described above; it does not require
asking the human to select LXC again. Existing authorization covers ordinary
DEV construction choices. Apply the declared cognition policy (its documented
default when no override is supplied), and request credentials only if the
selected engine actually needs them and they are unavailable through authorized
references. A public domain, paid API key or renewed DEV approval is not a
universal prerequisite for the first local construction.

The first agent response should briefly restate the destination and result,
then begin the authorized prerequisite checks. It explains the composition and
first proof, and proceeds to construction when the required access and mandate
are available. Missing code is work to perform. A choice of internal schema or
implementation method is for the agent to make within the contracts. A missing
business intention, access right or conflicting requirement calls for a focused
question about that point, while independent authorized work continues.

## What to ask for at completion

Ask the agent to show the universe's identity and location, its functional units
and their responsibilities, a real operation demonstrating the requested
purpose, and the recovery result. Keep source checks, installation, observed
operation and human acceptance distinguishable.

This request starts a human–agent construction process. It does not imply that
a prebuilt image or a complete automated deployment is supplied by this
documentation repository.

## Reuse after the first success

Once there are verified units or universes worth duplicating, it is recommended
to put their reusable artifacts in a registry, with immutable identifiers and
links to the composition and proof. The
[reference procedure](../procedures/01-REFERENCE-UNIVERSE.md#registry-after-verification)
explains what to retain. Each duplicate receives its own identity and state;
secrets and live business data are not a reusable template. A registry can be
organized later and is not needed to start the first construction.

Continue with the [reference universe procedure](../procedures/01-REFERENCE-UNIVERSE.md)
and the [ideal scene](../IDEAL-SCENE.md).
