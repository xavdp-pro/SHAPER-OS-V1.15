# Rules 13–22 — Services, interfaces and typed quality

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
The original rule identifiers, scope and binding force are unchanged.

<a id="rule-13"></a>
### Rule 13: Hybrid WireGuard Private Mesh Network & Mandatory Peer Naming
* All distributed nodes (universe hosts, cloud VPS, bare-metal Proxmox) join the private encrypted mesh:
  * Central gateway on the declared `<MESH_SUBNET>` parameter.
  * Dynamic peer key registration.
  * Persistent keepalive (`PersistentKeepalive = 25`) for firewall/NAT traversal.
<a id="rule-13-peer-comments"></a>
* **Mandatory Human-Readable Peer Comments**: Because raw WireGuard only uses cryptographic hashes, every AI agent or engineer registering a peer on the gateway (`wg0.conf`) MUST ALWAYS precede the `[Peer]` block with an explicit comment tag:
  ```ini
  ### Client <hostname> (CT <vmid> on <host>)
  [Peer]
  PublicKey = <CLIENT_PUBLIC_KEY>
  AllowedIPs = <CLIENT_MESH_IP>/32
  ```
  Anonymous or untagged peer blocks are strictly prohibited to ensure instant auditability and DNS mapping.

---


A distributed realization declares and proves its WireGuard mesh. An isolated first local construction does not invent remote peers or require a mesh before it has a distributed dependency.

<a id="rule-14"></a>
### Rule 14: Efficient Visual and Programmatic Control
* **Priority to Deterministic Control (No LLM Tokens)**: Use deterministic X11 commands through the selected desktop-control adapter for standard application launching and document conversions.
* **Multimodal Visual Mode through a Declared Adapter**: Use screenshots and cursor actions only when interacting with legacy graphical interfaces lacking programmatic APIs.

---

<a id="rule-15"></a>
### Rule 15: Media Art Direction & Industrial Realism
* Natural warm sunlight, healthy green vegetation, genuine professional expressions, and dual representation of human operators and sustainable infrastructure.

---

<a id="rule-16"></a>
### Rule 16: Multi-level backup (container → files tar.bz2 → database → git → S3)
These five levels cover distinct recovery needs; missing a required level is a gap. Their implementation belongs to the realization.

| Level | What | How (Shaper / Podman spirit) |
| :--- | :--- | :--- |
| **1. Infra — entire container** | The universe container as a whole — the LXC/CT (or VM), or the outer Podman container of a `nested` universe | Host snapshot (`vzdump` / ZFS / Proxmox). For `nested`, a consistent export of the stopped outer container plus its declared volumes is the baseline; prove its restoration on the selected host. Checkpoint/live migration is a separate optional capability, not a universal prerequisite or implied proof. This outer recovery does not replace the inner levels. |
| **2. Files — persistent volumes** | Only what must survive a recreate | Archive **Podman bind-mounts** (`<univ>/sav/*`, `/data/<slug>/` persistent volumes) as **`tar.bz2`** (pbzip2), like turbinobash app backups. **Exclude `nosav/`**, caches, image layers, `node_modules`. |
| **3. Databases** | Every functional Podman's relational / vector state, consistent and separate | Run `mariadb-dump` independently for every functional Podman's private MariaDB — inspect the selected image’s actual client names (`mariadb`/`mariadb-dump` or its documented compatible alternatives); a script falls back to `mysqldump` only where that name still exists. Plus Qdrant snapshots and JSONL rotation where declared. A recovery point is incomplete if one functional database is omitted, and no live volume tar substitutes for a crash-consistent dump. |
| **4. Git** | Code and architecture | Immutable tagged repo. Never treat git as a data backup. |
| **5. S3 / R2** | Off-site copy of 2+3 (and optionally 1) | Encrypted archives (AES-256-GCM), cold bucket (Cloudflare R2 / Glacier-class). Copies **the tar.bz2 and dumps**, not a second git clone pretending to be backup. |

**Files (level 2) are the volumes, not the overlay.** Recreating the Podman container from a tagged image + restoring `sav/*.tar.bz2` + DB dump **is** the inner restore. Level 1 is the outer safety net (CT gone). With 1–5 together, PCA/PRA data path is covered.

**The object key is derived, never improvised.** Each function-owned database
recovery point is stored below
`r2://<instance-id>/functions/<functional-slug>/mariadb/<recovery-point-id>/`.
That prefix contains the encrypted `mariadb-dump`, a manifest naming the
universe instance, functional slug, schema/version and capture time, the
plaintext artefact digest recorded before encryption, and the restore receipt.
The encryption key never travels in that prefix (Rule 12). This derivation lets
an agent enumerate the manifest and restore the correct database without
learning an application's internal layout.

<a id="rule-16-archive-hygiene-scope"></a>
Rule 12 (archive hygiene: no autoindex, basic auth, TLS) applies to any `tar.bz2` that leaves the host.

---

<a id="rule-17"></a>
### Rule 17: Mandatory TTS Phonetic Dictionary, Acronym Expansion & Fine Word Karaoke
* **Universal TTS Text Normalization**: Before dispatch to the selected TTS provider, the realization applies a locale-aware text normalization contract:
  * **Acronym Expansion**: Technical acronyms (`API`, `SQL`, `GED`, `URL`, `SSH`, `HTTP`, `HTTPS`, `CSV`, `PDF`, `TTS`, `STT`, `LLM`, `IA`, `UI`, `UX`, `OS`, `RAM`, `CPU`, `DB`, `IP`, `CLI`, `JSON`, `SDK`, `DNS`, etc.) are converted to hyphenated letters (`A-P-I`, `S-Q-L`, `G-E-D`, `C-S-V`, `J-S-O-N`) to force clean, natural letter-by-letter pronunciation instead of garbled phonetics.
  * **Markdown & Artifact Stripping for Voice**: Code blocks (`` ``` ``), inline backticks, image links (`![...]`), raw markdown URLs, and emotion tags (`[calm]`, `[excited]`) are cleanly stripped from the spoken audio pipeline while preserving full rich markdown in the written chat bubble.
  * **Locale Symbol Expansion**: Symbols like `%`, `&`, `@`, `+` are expanded into their natural locale equivalents (`pour cent`, `et`, `arobase`).
* **Strict Fine-Grained Word-by-Word Karaoke Invariant**:
  * **Zero Giant Block Highlighting**: Highlighting of entire sentences/paragraphs (`grain: 'sentence'`) is strictly forbidden. The player and markdown viewer MUST always enforce fine word granularity (`grain: 'word'`).
  * **Clock-Synchronized Word Weighting**: For streaming providers without native word timestamps , timings are computed by the realization’s word-timing estimator using word length and punctuation weight, dynamically rescaled against actual PCM playback duration.
  * **Fluid Visual Reading**: In the rich-text viewer and inline karaoke renderer, only the exact word currently being spoken (`activeIndex`) is illuminated in real-time, providing a smooth, realistic, and responsive reading experience.

---

<a id="rule-18"></a>
### Rule 18: Primary Admin Account Onboarding Protocol (Zero Unsolicited Dummy Users)
* **Primary Admin for a Human Login Surface**: When the declared composition provides a human login/admin surface, such as Helm, complete its primary-admin onboarding after bootstrap and health checks. A headless reference without that surface does not require adding Helm, a human account or a login URL merely to satisfy this rule. Functional-unit identities and their credential requirements still apply.
* **Reuse Authorized Choices**: For that human login surface:
  1. Obtain the human’s chosen primary Admin identity and secure credential through the authorized channel. Reuse values already supplied; ask only for genuinely missing choices:
     * Preferred **Email address** (e.g. `<operator-email>` or custom).
     * **First Name / Display Name**.
     * Secure **Password**.
  2. The agent MUST NOT leave unverified, dummy, or hardcoded mock users in the system database.
  3. The agent provisions the account in MariaDB (`users` table) with `role: 'admin'`, seeds their dedicated workspace directory (`<WORKSPACE_ROOT>/<USER>`), generates the sovereign `CONTEXT.md`, and confirms the login URL to the human.
* **Zero Legacy Demo Clutter**: Unrequested demo guest accounts are strictly prohibited in the default base source code, registries, and production instances.

---

<a id="rule-19"></a>
### Rule 19: Dual Semantic Register & The Toggle Law (Zero Jargon in Simple Mode)
* **Two Abstraction Levels for Every Output**:
  * **Simple Mode (Decision-Maker / Business User)**: Natural language focused strictly on actions, results, and deliverables (e.g. *"The customer report is ready and filed in the document library"*). Internal system jargon (`P1`, `P2`, `P3`, `Maestro`, `KovZu`, `Podman`, `Redis`, `Tokens`, `Endpoints`) is strictly banned. Allowed positive anchor words: *Sovereignty, Autonomy, Tailored, Deliverable, Secure, Verified*.
  * **Technical Mode (CTO / Developer)**: Full observability, job IDs, execution trees, HTTP status codes, queue metrics, and JSONL log streams.
* **Structural Contract, Not Just Vocabulary**: Avoiding jargon is necessary but not sufficient. Every Simple Mode restitution MUST answer three questions in order: (1) *what was done*, (2) *what artefact it produced and where it is*, (3) *what decision, if any, is expected from the human*. A message that respects the word ban but leaves the reader unable to act violates this rule.

---

<a id="rule-20"></a>
### Rule 20: Typed Closed-Loop Quality Gate (Verification Before Delivery)

<a id="rule-20-functional-test-means"></a>
* **Construction includes functional verification.** Before building, the
  constructing agent in the human-agent tandem inventories the scoped features
  from the applicable intents, rules and manifest, including inherited base
  capabilities and specialization. The same checklist defines expected results
  before implementation and carries actual execution evidence after assembly.
* **Test means follow the delivered interaction.** For every feature, the agent
  determines, prepares and verifies the tools, access, equipment, test data and
  observation channels needed to exercise its real usage. This is open-ended:
  command-line features require actual commands; APIs require actual requests;
  web interfaces require a controlled browser (for example Playwright); mobile
  applications require control of the installed app on an authorized device;
  physical integrations require appropriate control/stimulation and independent
  observation of the equipment. No fixed technology list limits this obligation.
* **Exercise every scoped feature on the assembled target.** The constructing
  agent executes the scenarios through their delivered surfaces and verifies
  downstream results outside the producer. Test each exposed contract and the
  cross-surface journey where applicable. A build, unit suite, health endpoint,
  screenshot or API success alone cannot stand in for the complete user journey.
  After correction, rerun the failed scenario and affected dependent scenarios.
* <a id="rule-20-record-what-actually-happened"></a>**Record what actually happened.** Each checklist item carries the target and
  source version, execution date, steps, expected and observed results, actual
  evidence reference, execution actor and coverage limits. Independent review
  supplements the agent's own functional run; human acceptance remains separate.
* **Missing test means are an explicit gap, never a pass.** Inspect available
  means first and prepare what the existing mandate authorizes. If required
  hardware, access or authority is missing, record NOT VERIFIED, the blocker and
  the smallest operator action needed; continue other authorized checks. No new
  spending, unauthorized external call or physical actuation is implied.
  Simulators/emulators qualify only what they actually exercise, never an absent
  real device or connector. Human-assisted execution is attributed honestly.

* **Pre-Delivery Verification by Deliverable Type**:
  * No job or generated output can transition to status `COMPLETED` in `@shaper/pkg-queue` without passing its typed verification contract:
    * **Code & Scripts**: Native unit test suite for the selected language, linter and disposable execution environment for the artifact. This test environment does not impose a sandbox on the authorized DEV lead agent.
    * **Documents & Spreadsheets (PDF, XLSX, DOCX)**: Schema validation, mandatory metadata presence, arithmetic consistency checks (e.g. Totals HT + VAT = TTC).
    * **Data & Imports (CSV, JSON)**: Column typing, primary key uniqueness, provenance validation.
    * **System Actions & External Dispatch**: Payload schema check, dry-run simulation when supported, then the authorized real effect and independent downstream evidence. A dry run alone cannot prove delivery.
  * In case of failure, the job transitions to self-correction or alerts the operator with explicit machine-verifiable diagnostics.
* **Isolation Is Required by the Contract Type, Not by the Rule**: an ephemeral sandbox exists to contain **execution**, so it is mandatory only where the verification actually runs the artefact — the `code` contract. Documents, data and actions are verified by schema, arithmetic, typing and provenance checks, which execute nothing untrusted and therefore run in the verifying process itself. Demanding a container for those buys no safety and costs privilege, deployment weight and latency. A brick that only produces documents must not be granted runtime access in the name of this rule.
* **No Untyped Deliverable**: A job whose output type has no declared verification contract MUST NOT be silently marked `COMPLETED`. It is held in `NEEDS_CONTRACT` and escalated to the human, who declares the contract once — thereafter it is reusable for that type. Rule 0G applies: an absent contract is never a reason to pass.
* **Activation Follows the Lifecycle**: DEV may record `NEEDS_CONTRACT` while constructing an unfinished typed gate, but cannot call the affected result verified or promote it. The realization declares and tests its enforcement switch, such as `QUALITY_GATE_ENFORCE=1`. Finalize enforcement during dedicated hardening after integrated acceptance and prove it before production. No real-client production action bypasses its typed evidence contract.

---

<a id="rule-21"></a>
### Rule 21: Distributed Multi-Agent Delegation Matrix (Abstract Capacity Classes)
* **Abstract Capacity Classes (Vendor-Agnostic)**:
  * Maestro is an orchestrator, supervisor, and auditor; it NEVER executes heavy transformation code directly.
  * **`heavy-engineering`**: High-reasoning architecture, multi-file refactoring, autonomous code generation.
  * **`rapid-iteration-ui`**: Interactive GUI components and visual refinement.
  * **`infra-ops`**: Vulnerability scans, system administration, container orchestration.
  * **`fast-eval`**: Streaming acknowledgments, low-latency text classification.
  * *The concrete mapping from capacity classes to actual execution engines (e.g. CLI agents, local ONNX models, bridge daemons) is declared in `manifest.json` and can be changed without modifying the doctrine.*
* **Human-in-the-Loop Classes Are Not Auto-Dispatchable**: A capacity class whose engine requires a human at the keyboard (interactive IDE) is declared `interactive: true` in the manifest. Maestro never auto-dispatches to it; it queues the task as `AWAITING_HUMAN` and notifies the operator. Autonomous classes and interactive classes are never mixed in one dispatch decision.

---

<a id="rule-22"></a>
### Rule 22: Automatic Semantic Memory Ingestion & Multi-Tenant Vector Isolation (RAG)
* **Continuous Passive Knowledge Capitalization**:
  * Any validated file deposited in `/data/ged` emits an asynchronous event that triggers automatic chunking and vector embedding into Qdrant using a sovereign local embedding model qualified and recorded by the realization; an ONNX runtime is a possible implementation.
  * **No silent degradation**: if the sovereign embedding model is unavailable, ingestion fails loudly and the document is queued as `PENDING_EMBED`. A lexical or hash-based placeholder vector MUST NEVER be written into a semantic collection (Rule 0G).
* **Strict Multi-Tenant Isolation**:
  * <a id="rule-22-isolated-qdrant-collection"></a>Each Universe owns its isolated Qdrant collection. An agent can only query its own vector namespace.
  * Parent Supervisor universes only consume aggregated metrics and structured summaries; they NEVER access raw child vector collections directly.

---


## Reading continuation

[Previous part](03-EXECUTION-AND-CONTAINMENT.md) · [Next part](05-REPAIR-AND-DATA.md)
