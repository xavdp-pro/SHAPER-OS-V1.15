# First construction and later reuse

Direction: **[MANDATE]** operator clarification, 5 October 2026, for first use of
the framework by an agent with no prior project context.

## Start from the documented intention

SHAPER OS deliberately contains no implementation code. The construction agent
reads its intentions, applicable laws, relationships and profiles, then produces
the concrete implementation needed for the human's request. This makes explicit
the [23 September direction](2026-09-23-AGNOSTIC-NO-CODE.md), especially points
3 and 4. A pre-existing SHAPER implementation, image or code repository is not
a prerequisite to beginning construction.

The human can start with a simple request naming a universe and a destination,
and add intentions for further functional units when already known. The agent
organizes the composition, derives concrete implementation contracts, writes
the code in a separate realization workspace, builds it and verifies the result.
It chooses unspecified implementation details within the applicable obligations;
it does not invent the human's authority or change an adopted requirement.

The hosting prerequisite is an available Podman or LXC environment capable of
hosting the selected composition, with authorized access and sufficient resources.
Local work uses local access; remote work needs authorized SSH access. The agent
checks the actual capabilities and prepares dependencies within the mandate.
The current construction profile retains Podman functional units with a private
MariaDB for each; LXC or Proxmox describes the outer hosting choice.

## Reuse follows construction and proof

Once verified units or universes are useful to duplicate, a registry is
recommended to retain and distribute their immutable artifacts with their
versioned composition and qualification records. It can be set up later.
A registry and an already qualified reference are not prerequisites to building
the first reference. Existing artifacts may be reused when suitable and verified;
the agent can also build a fresh realization from the contracts.

This direction concerns new construction from zero. It explicitly removes a
pre-existing registry as an entry requirement for that work, including when
reading V1.14 Rule 3's registry prerequisite. Existing deployed realizations
retain their identified distribution and promotion contracts; this clarification
does not authorize changing their operating arrangements. Identity isolation,
private data ownership, restoration and qualification obligations still apply.

## Reading and proof boundary

First-use documentation must explain the prerequisites, the agent's construction
responsibility and the route from a short request to observed results without
depending on private conversations or an existing implementation. Named external
law remains reading material where applicable; reading it does not require
installing its historical code.

Documentation clarity and generated code do not establish runtime success.
Record what was built, tested, installed, observed and accepted separately.
An independent reader should be able to identify the first useful actions and
the precise question, if any, that needs the human's decision.
