# Construction, Hardening and Production Lifecycle

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

DEV, TEST and PROD are separate universe instances and data scopes. A local first build is DEV; a public console or successful model reply does not make it production.

## DEV: build the integrated function

The tandem actively directs authorized construction and follows changing interactions. The lead agent uses full noninteractive provider-equivalent execution without a CLI sandbox or repetitive approval questions within the mandate. Generate missing implementations, test components, correct defects and build the complete workflow.

Design security from the outset: roles, jurisdiction, resource/data boundaries, sensitive operations and expected evidence. Implement what is necessary for correct functions, separation and preservation of data during DEV. Avoid freezing every granular permission before interactions are understood or repeatedly patching permissions by trial and error. Keep the designed boundaries recorded as the system evolves.

Use dedicated real test mailboxes and test credentials for integration; never reuse production mail or leak production secrets into DEV/TEST. A unit simulation may support code testing, but only actual operations prove an integration capability. Keep DEV disposable except the source and evidence explicitly retained.

## Integrated acceptance, then dedicated hardening

Once the tandem accepts the integrated functions and their interactions, use that complete view to finalize and enforce the roles and jurisdictions designed during DEV. The tandem decides and implements production permission envelopes per action or action type: resources, operations, data and effective runtime rights proportionate to the task. This does not prescribe one isolation technology.

Authorize before dispatch. Maestro's schedule grants no extra rights; Queue grants none; the bridge executes the exact envelope. Infrastructure must enforce actual permissions: a prompt, selected directory or claimed role alone is not runtime isolation. Already-authorized actions proceed without repeated approval requests; a genuinely new mandate remains a human decision.

Replay the accepted integrated workflows under the production rights, verifying permitted effects, boundary enforcement and usable results. A set of security settings alone does not prove that the system still functions.

## TEST: rebuild, qualify and destroy

1. Create a blank system-container universe, LXC or nested Podman as selected; do not reuse the DEV filesystem.
2. Apply the qualified host profile, install declared runtime prerequisites and retrieve the pinned realization source.
3. Bootstrap test Vault/state and build every image from source without inherited caches. Register the class in its own fleet map for promotion.
4. Deploy by the manifest/topology, run native, real integration, regression and typed deliverable checks, including the final permissions of the candidate production profile.
5. Verify recovery with the declared data and secret-key custody. Record exact inputs, revisions, observations and gaps.
6. Retain the required evidence and destroy the disposable TEST container and declared volumes. Parallel TEST instances may not share disks or production mail.

Recovery has three clocks: cached-image start, image rebuild/pull from zero, and data restoration. Host provisioning is additional. Public claims remain qualitative (“fast and structured”); measured observations belong in operational evidence with their conditions and exclusions.

## TEST initial data

Under [Rule 10](../../RULES.md#rule-10), a blank rebuild may receive declared
initial data; it does not inherit DEV state. The realization versions its schema,
migrations and fixture/seed definitions with the source, records their revisions
or digests and expected contents, and materializes them into the fresh TEST
units through their declared bootstrap interfaces. Generate deterministic
synthetic data where appropriate, or retrieve a pinned non-sensitive reference
dataset with its provenance and permitted use recorded. This supplies known
inputs without reusing a database, image cache or undeclared filesystem state.

Create fresh TEST identities and credentials through the authorized test bootstrap;
never seed production identities, keys, secrets, mailbox state or a production
database. Keep secret values out of fixture sources and evidence. A test of
restoration uses a separately identified backup of controlled test state with
its declared key custody; distinguish this recovery phase from the initial clean
build. Record both the initial seed and later mutations so the result can be
reproduced and cleanup can remove only owned disposable state.

A catalog fixture exercises known inputs; it cannot substitute for a required
real downstream service or authorize external actions. Use dedicated real test
accounts for those checks under the [proof contract](PROOF.md).

## DEV to TEST evidence handoff

**[EXPLANATION]** The following record organizes the existing lifecycle and
[typed proof obligations](PROOF.md); it adds no release authority. Keep it with
the candidate realization, using evidence links and explicit outstanding gaps
instead of treating checked boxes as proof.

| Handoff item | Record or verification |
| :--- | :--- |
| Candidate and scope | Mandate, governing revision, realization source commit, composition/profile, affected units and typed acceptance criteria. |
| DEV function and security | Native and integrated results, independent effects, tandem's functional acceptance, designed boundaries and remaining hardening work. |
| Rebuild inputs | Qualified host profile, pinned source/dependencies, topology and actual readiness dependencies, versioned test data, fresh TEST credentials by reference, owned disposable volumes. |
| TEST execution | Evidence of blank construction and images built without inherited caches; real native, integration, regression and deliverable results with failures and limitations visible. |
| Hardening and recovery | Enforced production action/type policy, replay of accepted workflows, relevant refusal boundaries, restoration and key-continuity observations; name any still-unqualified obligation. |
| Disposition | Retained evidence and observed TEST cleanup; exact qualified candidate/artifacts, remaining gates and existing promotion mandate or genuinely missing decision. |

Record entries as they become available. Early TEST runs may qualify individual
paths while construction continues; they do not claim full candidate acceptance.
Dedicated production hardening follows integrated functional acceptance, and the
final qualification replays the accepted workflows under that policy. First
isolated DEV construction does not itself request TEST or production promotion;
apply later stages when the mandate reaches them. No handoff record authorizes
copying DEV state into TEST or production.

## PROD: durable state and authorized change

Create production once with its own credentials, domains and durable mounts. Promote only the exact qualified immutable source/artifact after tandem acceptance. Updates use [Rule 25's canary](../../RULES.md#rule-25) and the typed deliverable gates, not just health and a beat. Retain data, snapshots/dumps and tested restoration before a schema change; apply expand/contract migration and the recovery plan of Rule 30. Rollback of code alone cannot undo every data change.

Never promote by copying files from DEV or deploying an unqualified moving branch. Production retirement and recovery obey parent/root authority and bounded repair. Cleanup removes only owned disposable environments; production state is not garbage collection.

See [LAW](../../LAW.md), [RULES](../../RULES.md), [Proof](PROOF.md), [Fleet](../architecture/FLEET.md) and the [common bridge contract](../intents/cognition-bridge.md).
