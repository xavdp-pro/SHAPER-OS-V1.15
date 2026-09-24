# Reference Universe Procedure

Identifier: **Procedure 01**.

Status: **[EDITORIAL]** proposed construction procedure for this V1.15
documentation candidate. It records the operator's 24 September direction; it
does not certify an existing image, amend an operational law, or provide an
executable deployment recipe. Read the [governing-corpus map](../GOVERNING-CORPUS.md)
and the target realization's exact governing revision before acting.

## Purpose

Provide a generic base container and its declared functional units, configured,
working and tested against the applicable contracts. Its versioned composition
is the reusable starting point that a project deploys before adding its own
functions. A base image alone does not include external state or qualification
evidence; a running container is not copied with its identity and live data.
The reference itself contains the base functional units only: no runtime AI
agent, Cognition Bridge or project-specific business function.

The goal is to start each project quickly from a dependable, reproducible base
instead of rebuilding or inheriting an obsolete one. As construction agents
improve, it is desirable to revisit this base periodically—for example after
three or six months—by asking current agents to rebuild it, rerun the tests and
recheck the applicable contracts. The comparison is against the qualified reference and
observed results, not an assumption that a newer agent is automatically better.
Adopt a replacement only when it preserves existing commitments and passes its
own qualification; keep the previous reference identifiable for recovery.

## Sequence

1. **Resolve the governing target.** Record the requested realization, operator
   mandate, exact governing revision, adopted decisions, profile, unit contracts
   and the source revision/digests of any artifacts proposed for reuse. Compare
   later applicable decisions with an older pinned base. A reused image cannot
   silently waive an obligation adopted after that image was built.
2. **Check whether a qualified reference exists.** Locate its immutable artifact
   digests, versioned composition, qualification record and supported profile.
   A running container, a successful build or a healthy endpoint alone is not
   a qualified reference. If it does not exist, build one before cloning any
   derived universe.
3. **Construct the isolated reference.** Create the profile's declared base
   functional units, their identities, state owners, storage, dependencies,
   permissions and startup/recovery contracts. Under the preserved
   [September container/MariaDB profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md),
   that means Vault, Logger, Queue and Maestro, each in its own runtime
   container with its own private MariaDB and scoped identity. No agent or
   Cognition Bridge is installed in this reference. A derived project may later
   add them under its own declared contracts. Another profile needs
   explicit approval and a mapped set of obligations; it is not inferred here.
4. **Configure and test the composition.** Check bootstrap order and identity
   continuity, unit readiness, authorized exchanges, persistence, duplicate and
   retry behavior, degraded operation, evidence of real effects, backup and
   proven restoration. Record observed results and failures against the
   contracts. Resolve gaps before calling the reference qualified.
5. **Freeze a reproducible reference.** Record immutable image digests *and* the
   versioned composition, configuration schema, migrations, qualification
   evidence and provenance. An image alone cannot contain the proof of external
   databases or the contract of a multi-unit universe. Publish a reference
   identifier only after the required checks pass.
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

## Decision gates

If the governing revision, applicability of a newer decision, unit contract or
source state is unresolved, pause the affected construction and ask the
authorized owner. A legacy prototype is not a reference merely because it ran.
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
