# Rules 6–12 — Agents, execution, containment and recovery

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
The original rule identifiers, scope and binding force are unchanged.

<a id="rule-6"></a>
### Rule 6: Targeted Agent Bootstrapping (Token Optimization & Zero Idle Waste)
* Every AI agent is bootstrapped with an isolated, targeted context file (`ctx-universe.md`).
* Never re-inject entire system rulebooks into execution prompts; send the prepared role-specific context, current deltas/instruction and action evidence needed for that execution. Reconstruct missing continuity before action.
* Leverage prompt caching, local deterministic idempotence checkpoints in the owning unit’s durable database, and zero token consumption when idle.

<a id="rule-6-decision-hygiene"></a>
**Decision hygiene is derived into the role, not carried as a second rulebook.**

* The designer translates intent, explicit values, people's rights and effects
  on others and the environment into scoped decision constraints. An agent's
  ethical interpretation never grants additional authority.
* The role's checks distinguish runaway goal pursuit, unwarranted inhibition
  and incomplete understanding. Responses consider both action and inaction,
  current evidence and the conditions under which prior experience applies.
* Prepared responses declare triggers, preconditions, current authority,
  deadline, review conditions and a permitted alternative. A response outside
  its validated context is not automatically replayed. Urgency does not expand
  permission; unknown situations require bounded action or escalation within
  the mandate, not invented facts or unlimited deliberation.
* Reliability includes a required deadline. Strict timing needs a bounded,
  tested execution path; an assumed model latency is not a guarantee.
* Firmness holds rights, current mandate and binding limits; permeability admits
  new evidence and revision of interpretations. A counter-view may challenge an
  interpretation or propose a rule change, never enact that change without its
  authorized owner. Agreement is not permission. Recheck effective authority at
  execution, including after review; record unresolved disagreement and provenance.
* Integrity keeps declared purpose, authority, commitments, action and evidence
  coherent and discrepancies visible. Internal consistency alone does not justify
  a goal. Disclose unmet commitments and affected dependencies; repair or revise
  through the authorized owner without rewriting evidence or fabricating success.
* External retrospective review preserves observations and provenance, compares
  outcomes and revises context-specific conclusions. Governing changes remain
  deliberate and owned; the acting agent never self-amends its authority.
* Qualification under Rule 20 exercises appropriate initiative, justified
  restraint, missing information, changed context and time pressure through the
  actual harness. Reciting the rule is not behavioral proof. The
  [operating contract](../../docs/agent/OPERATING-CONTRACT.md#decision-hygiene-qualification)
  specifies the evidence boundary.

---

<a id="rule-7"></a>
### Rule 7: Engine Defaults Are Measured, Never Declared
* **No default model is written in this canon.** The rule that used to live here
  named specific models and their flags; every one of them aged, and the canon
  aged with them. A default that must be edited when a vendor ships a new version
  is not a rule, it is a cache.
* **What is binding instead**:
  * Each brick declares the cognition its work requires — capacity class, depth
    `D0`–`D4`, throughput `T0`–`T3`, degradation policy — in its `INTENT.md`
    ([`docs/architecture/COGNITION.md`](../../docs/architecture/COGNITION.md)).
  * At every deployment the agent enumerates the engines actually reachable from
    the target host, sends a bounded ping, measures, and selects according to the declared cursor among engines that satisfy depth, throughput and the actual-task probe.
  * **Cost and performance are two cursors, reconciled by fact and by
    declaration — never by a hidden formula.**  The procedure:
    1. **The contract eliminates.** An engine that fails the declared depth,
       throughput or correctness probe is out at any price.
    2. **Dominance eliminates.** An engine both more expensive AND less
       performant than another measured engine is discarded — that is a fact,
       not a policy. What remains is the frontier, where every choice is
       legitimate.
    3. **The universe declares its cursor** (`enginePolicy` in its manifest;
       absent means `frugal`):
       `frugal` — the cheapest engine on the frontier. Dominance makes it
       automatically the fastest of the cheapest, so free-tier ties resolve
       to measured speed, as before.
       `swift` — the most performant engine on the frontier; for voice and
       real-time universes, where a slow engine is useless at any price.
       `budget: <max cost per task>` — the most performant engine under a
       ceiling the operator declares. The number comes from the operator,
       never from this canon: a weighting constant invented here would be an
       unmeasured figure, and Rule 10 forbids those.
    **The probe is the contract.** An engine is measured on the shape of the
    work the universe will ask of it — for the base, write-a-file-then-reply,
    never a bare echo: an engine has passed the ping and then hung on the
    real task, answering generic text once stopped .
    Performance is **measured from the target host** — correctness on a
    bounded probe and observed latency/throughput — never a figure read from
    a vendor page or a public ranking. Published speed has already been wrong
    here: the fastest model on paper timed out twice from inside an LXC while
    a slower one did the work.
  * **The measurement is part of the deployment, not a preliminary.** An engine
    adopted without a recorded ping is an undocumented dependency, even when it
    answers: a healthy bridge proves the bridge, never the model behind it.
  * The selected engine, its measurement and the moment of measurement are
    written to the deployment log. **An engine chosen without a recorded
    measurement is an undocumented dependency** and fails Rule 0G.
* **Execution flags** belong to the bridge that wraps the CLI (Rule 34), declared
  and pinned in its image — not in this canon.
* **Ultra-fast engines** remain reserved for acknowledgment and voice micro-tasks
  and are never exposed as general agent chat models (Rule 0H, Rule 0K).

---

<a id="rule-8"></a>
### Rule 8: Universal Agent HTTP Contract

Every containerized agent exposes:

| Method and path | Meaning |
| :--- | :--- |
| `GET /api/health` | Service readiness and its private database connection |
| `POST /api/inject` | Context-bearing task injection |
| `GET /api/events` | Server-Sent Events for correlated live execution |
| `GET /api/metrics` | Structured events and latency metrics |

A cognition bridge additionally obeys [bridge status](../../docs/contracts/bridge-status.md) and the [common session/context/action contract](../../docs/intents/cognition-bridge.md). An endpoint's health never proves model execution, permission or the task's external effect. Provider-specific transport mappings belong in the selected adapter's concrete contract.

---

<a id="rule-9"></a>
### Rule 9: Strict Mailbox Isolation (Test/Dev vs Prod)
* All IMAP synchronization, categorization, and message testing must strictly target dedicated test mailboxes.
* Absolute protection against data corruption or unintended message operations in production.
* Centralized AES-256 encrypted credential storage in the Vault.

---

<a id="rule-10"></a>
### Rule 10: DEV, TEST, PROD and Three Recovery Clocks

Every universe keeps three decoupled lifecycle environments:

1. `<slug>-dev`: authorized construction and prompt tuning, in its separate workspace and data scope.
2. `<slug>-test`: a blank system-container universe, actual internal Podman units, appropriate mesh attachment when distributed, Vault injection and the full applicable test suite. Rebuild all images from source without inherited cache; pulling an existing image cannot prove a clean build.
<a id="rule-10-destroy-after-test"></a>
   After verified testing and retaining the necessary evidence, destroy the ephemeral test container and its declared disposable volumes. This proves reproducibility without leaving residue.
3. `<slug>-prod`: durable state, promoted immutable revisions, controlled atomic updates and verified continuity. Preserve production data and use the canary and migration rules.

Recovery has three distinct clocks: cached images and stack start; rebuilding or pulling images from zero; and restoring the data volume. Host/system-container provisioning is additional. They must never be collapsed into one performance claim.

<a id="rule-10-zero-duration-figure"></a>
The public formulation is **fast and structured recovery**, without a duration figure, even as a figure to refute. Its method is repeatable: encrypted socle, orchestration, restitution and proof. The time depends on the host, cache and data. A measured operational note may state an observation with exact conditions, exclusions and data/cache state, explicitly not a promise.

Security is designed from the outset; implement functional/perimeter necessities while the tandem directs DEV. After integrated functional acceptance, finalize and enforce the designed production roles, jurisdictions and per-action/type rights, and replay accepted workflows under them before promotion. See [lifecycle](../../docs/agent/LIFECYCLE.md).

---

<a id="rule-11"></a>
### Rule 11: Two Levels of Containment and Recovery Integrity

* A universe is a system container with its own init, filesystem and packages. A brick is an application container built from an immutable image and **always runs under Podman**. Depth comes from nesting universes, never from a brick containing another container. No Docker runtime, installer or shared Docker image/network/store path is permitted.
* A class declares `shape: lxc` (default) or `shape: nested`. `lxc` uses a Debian LXC in the `lxd`, `liblxc` or `proxmox` host family. `nested` uses a rootful outer Podman universe holding its own Podman, image store and functional bricks. Do not flatten the universe into host-level application containers.
* A machine may offer several host families, at most one per shape. Declare those families in the fleet map. The maker chooses its qualified recipe by the class's shape and the machine's family; shape and family are different fields. `liblxc` is the family token, not `lxc`; `nested` is the family token, not `podman`.
* For Proxmox, the realization verifies Debian compatibility and enables the required nesting/keyctl settings. LXD uses an applied nesting-capable profile. Raw liblxc declares its nesting, cgroup, network and device requirements. A nested realization determines and proves its storage driver, user/cgroup namespaces, delegation, capabilities, device access and network configuration on the selected host. No historical laboratory flag set is a universal recipe.
* Local construction requires an authorized Podman or LXC-capable host; remote construction requires authorized SSH. If no suitable substrate is available, identify the architecture choice and its impact before changing host storage, hypervisor or network configuration. Existing human authorization suffices; an ordinary package dependency is construction work.
* The operator attests repeated practical deployments, including nested Podman. A new candidate still qualifies its own build, inner containers and recovery on its selected host. Live migration, checkpoint/restore, high availability and host-loss survival each require their own proof and are not implied by nesting.
* Presence of a binary is not capability proof: launch a disposable universe, run a real Podman container inside it and execute an actual image build step. Record what was observed.
* A universe-management tool such as PodMesh is optional and grants no authority. If selected, the maker's typed recipe invokes its declared operations and verifies effects from outside. Its per-host node and active manager are distinct from the governor and maker; the active manager holds a current externally issued activation lease/epoch. Qualify only the operations actually used.
* First boot updates the selected system-container OS and installs the declared packages, shell configuration and host modules. The realization supplies this recipe; no skeleton files are assumed to ship with the OS documentation.

<a id="rule-11-nftables-inside-the-universe"></a>
* Inner Podman networking requires its firewall dependencies, including `nftables` for netavark. Install and prove them inside the universe rather than relying on a host inventory.
<a id="rule-11-read-profiles-with-config-show"></a>
* Read actual applied LXC configuration (`lxc config show`, profile configuration or `pct config`); an information command that omits the profile cannot validate it.
<a id="rule-11-nesting-needs-a-restart"></a>
* A nesting change on an existing LXC requires the corresponding authorized restart before validation. Prefer declaring it at launch. Nested Podman namespaces/delegation are established when the outer container is created.
<a id="rule-11-declared-ports-are-free"></a>
* Compare declared listening ports with actual sockets before deployment. Distinguish the owned brick being replaced from a foreign holder. Identify a conflict and its owner; do not silently pick another port or stop an unrelated service. A shared network namespace, if chosen, is confined to the universe and never flattens the two containment levels. Every functional unit's MariaDB remains private, using its own socket/network boundary; do not expose several databases on one shared localhost port.

<a id="rule-11-what-is-restored"></a>
* Restorable identity consists of `manifest.json`, `cfg-image-lock.json` and declared volumes. Images are rebuilt from pinned source or pulled by digest, never treated as backup state. Complete restoration with the universe's own acceptance proof.
<a id="rule-11-a-brick-is-rebuilt-not-repaired"></a>
* Four operations remain distinct: **CORRECT** fixes a known error in controlled source; **REPAIR** restores non-reproducible database/volume state; **REBUILD** recreates reproducible runtime from a known-good image; **QUARANTINE** removes suspect runtime from service while retaining evidence. An in-place cleanup does not re-establish trust.
* Close the cause before rebuilding a compromised component. Incident order is: notice suspicion, reduce/freeze privileges, capture evidence, quarantine, identify cause, correct source, rebuild, test, obtain a counter-view, restore service, observe, deliberately retire/archive the old instance. This is distinct from DEV → TEST → PROD. Quarantine is a trust condition, not a fourth environment; a suspect instance never returns unchanged.
* A service start recreates the complete application container from its known image. Its declared non-reproducible volumes survive. A class may add bricks but may not invent an in-place patch as a fifth recovery operation. The [consulted-context doctrine](../../docs/design/CONSULTED-CONTEXT.md) explains the design/acting boundary.
<a id="rule-11-a-brick-runs-as-its-own-class-not-root"></a>
* Own application code runs as the unit's declared system user, with the same slug for system user, database and database user. Use a fixed numeric UID above 1000, build-time ownership and the correct runtime user. Scope ownership changes to files that process actually owns; never recursively chown another unit's database volume. Grant the specific low-port bind capability if needed instead of running the application as root. Upstream images retain their documented internal service identities; administrative root/Podman provisioning is a separate authorized path. Full DEV lead-agent execution does not make every application service root.

---

<a id="rule-12"></a>
### Rule 12: Secure Archive Distribution & Cold Recovery
* All archive transfers (`PROJECT.tar.bz2`, `REMOTE.tar.bz2`) must follow:
  * Multi-threaded compression (`pbzip2` or `tar -cjf`).
  * Zero directory listing (`autoindex off`).
  * Mandatory HTTP Basic Auth (`auth_basic` with hashed credentials).
  * End-to-end TLS encryption via Cloudflare Tunnel.
<a id="rule-12-what-a-backup-archive-never-contains"></a>
* **What a backup archive never contains, and what it never lies about** :
  * <a id="rule-12-key-does-not-travel-with-the-coffer"></a>**The key that opens the coffer does not travel with the coffer.** A backup
    carries the Vault’s encrypted persistent records; it never carries populated secret environment files, because those may hold
    `VAULT_MASTER_KEY`, and an archive holding both is the vault in clear text
    for whoever holds the archive. The key is restored from the operator's own
    separately held recovery-key record, never from the encrypted archive it opens. The realization documents key custody and tests that recovery path.
  * <a id="rule-12-backup-key-is-its-own"></a>**The backup's encryption key is its own key.** `PRA_ENCRYPTION_KEY` is
    generated for backups and for nothing else; it is required, and it is
    refused when it equals `VAULT_MASTER_KEY`. A backup encrypted with the
    vault's master key hands the vault's key to whoever breaks one backup.
    The key reaches `openssl` through the environment (`-pass env:`), never as
    a command-line argument readable by every process on the host — the same
    rule as a database password, which travels in `MYSQL_PWD`, never as `-p`.
  * <a id="rule-12-dump-not-taken-is-announced"></a>**A dump that was not taken is announced, never written empty.** The
    client is `mariadb-dump`, or `mysqldump` where only that one exists — a
    script that knows one name dumps nothing on the other host. A dump with no
    client, or no database declared for its scope, prints `SKIP` and says
    why; a required functional-unit database omitted this way makes the overall recovery point incomplete; a dump whose client fails, or whose output is empty, fails the backup.
    `2>/dev/null || true` on a dump is a zero-byte `.sql` archived as the
    database.
  * <a id="rule-12-archive-failure-is-backup-failure"></a>**The archive command's failure is the backup's failure.** A `tar` that
    ends in `|| true` followed by `{"status":"ok"}` is a report about a file
    nobody checked. The status line is printed after the archive exists, has a
    size and has a checksum, or it is not printed.
  * <a id="rule-12-complete-archive-is-kept"></a>**A failure after the archive is complete keeps the archive.** Cleanup
    on exit removes a partial archive, never a complete one that has been
    announced: a rotation that cannot run is a failure, reported over an
    archive that stays — "Backup created" on the log and an empty directory
    on disk is a data loss caused by housekeeping.
  * <a id="rule-12-failed-dump-leaves-nothing"></a>**A dump that failed leaves nothing behind.** The dump is written under
    a `.part` name and renamed only once it has a size; a client that dies
    half-way leaves no `.sql` for the next snapshot to archive as the
    database. A partial file left on disk is the empty-dump defect moved one
    run later.
  * <a id="rule-12-env-in-every-spelling"></a>**`.env` in every spelling.** `.env`, `.env.local`, `.env.<slug>`,
    `deploy/env`, `<slug>.env` — a credential may have been materialized under any of
    them, and the exclusion is `.env*` and `*.env`, never the bare name.
  * <a id="rule-12-client-call-proven-with-a-recorder"></a>**How the script calls the client is proven with a recorder.** The
    guard tests run the real scripts, the real `tar` and the real `openssl`
    against a throwaway layout; the one substitute is a recorder standing in
    for `mariadb-dump`/`mysqldump` on a PATH built from scratch, because what
    is under test is the call — which client name, where the password
    travels, what a failing or empty client does to the backup — and not
    what MariaDB answers. What MariaDB answers is the live test's business
    (Rule 0G), and the recorder never stands in for it there.

---


## Reading continuation

[Previous part](02-CONSTRUCTION.md) · [Next part](04-SERVICES-AND-QUALITY.md)
