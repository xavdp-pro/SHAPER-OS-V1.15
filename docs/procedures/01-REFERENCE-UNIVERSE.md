# Reference Universe Procedure

Identifier: **Procedure 01**.

Purpose: **[EDITORIAL]** guide the construction and renewal of a reusable
reference universe, following the operator's 24 September direction and
[5 October first-construction clarification](../../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md).
Use the [governing-corpus map](../GOVERNING-CORPUS.md) and the realization's
versioned contracts to connect this sequence to its concrete deployment tools
and operating evidence.

## Purpose

Build a first reference from the documented intentions and contracts, or reuse
a suitable qualified reference if one is available. The construction agent
produces the code and executable material in a separate realization workspace.
No existing SHAPER code repository, image or registry is required to start.
Use the [creation example's prerequisites](../examples/CREATE-A-UNIVERSE.md#what-needs-to-be-available)
to establish the destination and available means.

The result is a generic base container and its declared functional units,
configured, working and tested against the applicable contracts. Its versioned
composition is the reusable starting point that a project deploys before adding its own
functions. A base image alone does not include external state or qualification
evidence; a running container is not copied with its identity and live data.
The selected reference contains the four foundational units and the OpenCode
Cognition Bridge by default, as directed in the
[24 September decision](../../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md).
It does not contain a project-specific business agent or function.

The goal is to start each project quickly from a dependable, reproducible base
instead of rebuilding or inheriting an obsolete one. As construction agents
improve, it is desirable to revisit this base periodically—for example after
three or six months—by asking current agents to rebuild it, rerun the tests and
recheck the applicable contracts. The comparison is against the qualified
reference and observed results, not an assumption that a newer agent is
automatically better.
Adopt a replacement only when it preserves existing commitments and passes its
own qualification; keep the previous reference identifiable for recovery.

## Sequence

1. **Resolve the governing target.** Create the new realization record with its
   requested result, operator mandate, exact governing revision, local
   [LAW](../../LAW.md), [RULES](../../RULES.md),
   [boot](../agent/BOOT-CONTRACT.md), [operating contract](../agent/OPERATING-CONTRACT.md),
   adopted decisions, profile, detailed unit contracts
   and the source revision/digests of any artifacts proposed for reuse. For an
   existing realization, read its records before changing it. Use the
   [new-realization guidance](../GOVERNING-CORPUS.md#starting-a-new-realization)
   to distinguish applicable law from implementation the agent will create. Compare
   later applicable decisions with an older pinned base using the
   [current construction crosswalk](../GOVERNING-CORPUS.md#current-construction-crosswalk). A reused image cannot
   silently waive an obligation adopted after that image was built.
2. **Choose construction or reuse.** With no suitable reference, proceed directly
   to step 3 and create one. No prior artifact is required. When a reference is
   proposed for reuse, inspect its immutable artifact digests, versioned
   composition, qualification record and supported profile.
   A running container, a successful build or a healthy endpoint alone is not
   a qualified reference. Qualify the result before using it to derive another
   universe; absence of a reusable reference does not block its construction.
3. **Write and construct the isolated reference.** Derive the concrete unit
   interfaces, schemas, lifecycle and tests from the requirements below and
   their applicable sources. Write the code, container builds and deployment
   material outside OS. Create the profile's declared base
   functional units, their identities, state owners, storage, dependencies,
   permissions and startup/recovery contracts. Under the preserved
   [September container/MariaDB profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md),
   that means Vault, Logger, Queue and Maestro, each in its own runtime
   container with its own private MariaDB and scoped identity. Add the OpenCode
   [Cognition Bridge](../intents/cognition-bridge-opencode.md) as the default fifth
   unit under the same isolation contract and the
   [generic context/session obligations](../intents/cognition-bridge.md).
   A derived project may later add its business agents. Another profile needs
   explicit approval and a mapped set of obligations; it is not inferred here.
4. **Integrate, then harden the composition.** Design the intended security
   while constructing the units and exchanges. Implement controls needed for
   important functional requirements and the agreed DEV perimeter, keeping
   authorized development fluid. Check bootstrap order and identity continuity,
   unit readiness, exchanges, persistence, duplicate and retry behavior, degraded
   operation, evidence of real effects, backup and restoration. When the tandem
   accepts the assembled functionality and interactions, perform the dedicated
   [hardening phase](../intents/cognition-bridge.md#security-by-design-followed-by-a-dedicated-hardening-phase):
   finalize and enforce the roles and jurisdictions designed during DEV,
   implement action/type permissions and the required production controls,
   verify permitted and refused operations, and rerun the accepted integrated
   workflows under that production policy.
   Qualify the installed bridge's actual behavior under the intended execution
   policy. Record results and remaining work; functional acceptance alone does
   not qualify the reference for production.
5. **Freeze a reproducible reference.** Record immutable image digests *and* the
   versioned composition, configuration schema, migrations, qualification
   evidence and provenance. An image alone cannot contain the proof of external
   databases or the contract of a multi-unit universe. Publish a reference
   identifier only after the required checks pass. A local versioned record
   suffices to identify the first result; registry distribution can follow.
6. **Derive a new universe safely.** Instantiate from the qualified reference
   with fresh universe identity, scoped credentials, empty or explicitly migrated
   state, and its own persistent volumes/databases. Never clone Vault's secret
   identity or another universe's live business history. Recheck target-specific
   integrations and prove the derived universe's own operation before promotion.
7. **Rebuild when the reference changes.** A change to the governing rules,
   functional-unit structure, dependencies, storage, bootstrap, identity model
   or intended behavior triggers an impact review. If it affects the qualified
   composition, rebuild and requalify the base, then publish a new immutable
   reference identifier. Never mutate the old reference in place or silently relabel it
   compliant. Existing derived universes need a separate migration and
   requalification decision; a new base does not upgrade them automatically.

## From unit intentions to implementation

These are the responsibilities already described in
[units and dependencies](../learning/04-UNITS-AND-DEPENDENCIES.md) and the
[profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md), applied to first construction:

| Unit | Perimeter | Implement and verify |
| :--- | :--- | :--- |
| Vault | P1 | Protect secrets and deliver them only to authorized unit identities. Bootstrap from the external construction path; preserve key and identity continuity after restart and restoration. |
| Logger | P1 | Accept authenticated evidence, preserve its ordering and integrity, and issue receipts with an explicit meaning. A receipt does not certify the producer's actual effect. |
| Queue | P1 | Persist accepted work, lease it to authorized consumers and reconcile terminal acknowledgment. A lost acknowledgment or expired lease does not prove the effect is absent. |
| Maestro | P2 | Turn declared schedules into idempotent due occurrences submitted to Queue. Persist scheduling responsibility; without a schedule, create no work. |
| OpenCode bridge | P2 | Apply the [common session/context contract](../intents/cognition-bridge.md) through the [OpenCode profile](../intents/cognition-bridge-opencode.md): prepare context, resume/reconstruct sessions, refresh actions and checks, provide the mandated execution policy and observable outcomes. The four base units continue without cognition. |

For each unit, the agent writes the realization's specific contract: accepted
inputs and outputs, identity and permissions, private MariaDB state, dependency
readiness, duplicate handling, failure states, recovery and observable acceptance.
Select implementation details that satisfy those obligations, and retain the
source link for each requirement. The absence of source code, a schema or a
container recipe is the reason to generate it, not a requirement to locate an
older implementation. If a required policy or governing obligation is actually
undefined, name that particular decision and its owner before the affected step.

### Illustrative Example (Non-Binding / Demonstration Only)

A first integration proof can schedule one bounded test job that writes a known
artifact in a declared test workspace. The realization defines the test consumer,
its authority and durable operation identity; a separate test functional unit
uses the same private-storage profile. It is test apparatus, not a sixth
mandatory base responsibility.

Observe Maestro's occurrence, Queue's persisted work and lease, the consumer's
actual artifact and settlement, and the corresponding Logger evidence. Check
an unauthorized request is refused. Repeat the same operation and interrupt a
consumer after its effect but before acknowledgment: verify reconciliation
without a duplicated effect. Check restart persistence and restoration from a
declared recovery point, including Vault continuity and pending work.

Exercise the bridge separately with a real authorized engine and verify its
output outside the bridge, then observe that a cognition outage does not stop
the four base units. An unavailable engine remains NOT VERIFIED for that part.
This is a worked proof design, not a claim that these runs have already happened
or that one scenario qualifies every contract. Keep the full acceptance checklist.

## Registry after verification

Following the [5 October direction](../../decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md),
a registry is recommended when units or universes become useful to duplicate.
The first construction can be completed before that service exists.

Keep immutable image digests together with a versioned reference to the universe
composition, applicable profile, source revisions, configuration schema and
qualification evidence. An OCI image registry may hold the images while those
other records live in the realization repository. Record how to obtain both.
Keep secrets, unique identities and live data outside reusable artifacts.
Duplication instantiates the composition with fresh identities and state, as in
step 6; it does not copy a running universe's confidential history.

## Decision gates

If the governing revision, applicability of a newer decision, required policy or
source state is unresolved, pause the affected construction and ask the
authorized owner. Write missing implementation contracts from known obligations;
do not treat an uncreated implementation as missing authority. Continue independent
authorized work while a genuine decision is outstanding. A legacy prototype is
not a reference merely because it ran.
An operator-approved temporary deviation, where the governing law permits one,
must be scoped and recorded with an expiry, isolation and migration plan; it
must never be reported as full compliance.

The reference record should answer: **which rules and profile, which units and
artifacts, which identity and state boundaries, which tests and recovery proof,
which remaining gaps, and who accepted the result?** Keep source tests, reference
qualification, installation of a derived universe and real-use acceptance as
separate evidence.

Next: [materialization](../learning/05-MATERIALIZATION.md) and
[evidence, recovery and learning](../learning/06-EVIDENCE-RECOVERY-LEARNING.md).
