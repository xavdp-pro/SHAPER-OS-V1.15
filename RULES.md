# SHAPER OS & UNIV — Fundamental Engineering Rules & Architecture Invariants

<a id="canon-preamble"></a>
This file is the **canon**. It is read in full, never summarised, never replaced by a
pointer to itself. Rules are added, never removed to fit what the code currently does —
when intent and implementation diverge, record the gap in the realization and correct it; a gap does not waive the contract.

---

## How to read this file

**Rule numbers are identifiers, not priorities.** They are stable so contracts can refer to them precisely. Their order is the order in which they were written,
so a low number means "written early", not "matters more".

**Read the complete law before operational work.** These six rules orient the reading — they are what shape
judgement rather than convention:

| Rule | What it changes about how you work |
| :--- | :--- |
| **0G** | No fake, no fallback. A thing that cannot be done is reported, never simulated. |
| **0A** | Which perimeter you are in — P1 socle, P2 agents, P3 business — decides what you may touch. |
| **0B** | Nothing environment-specific is ever hardcoded. Everything is a parameter. |
| **32** | Perfect the generic base first; business specifics go on top of it, never into it. |
| **23** | Never modify your own running infrastructure. Repair comes from the level above. |
| **20** | Nothing is `COMPLETED` without passing the verification contract for its type. |

**Then go where your work is:**

| You are… | Read |
| :--- | :--- |
| building or changing a brick | 0A, 0B, 0C, 0D, 0E, 32, 33 |
| deploying or operating | 3, 10, 11, 12, 13, 16, 25, 27, 30 |
| working on agents, bridges, delegation | 0F, 0H, 0K, 6, 7, 8, 19, 21, 23, 24 |
| handling documents or data | 20, 22, 26, 31, and `docs/design/DOCUMENT-PIPELINE.md` |
| shipping to a client | 0G, 0J, 10, 18, 19, 25, 31, 33 |

---

## Binding force is uniform. Consequence is not.

These two statements are different, and only the first is about obedience:

1. **Every rule is mandatory.** None is a suggestion, none is skipped for convenience,
   none is optional because it is inconvenient today. That is [`LAW.md`](LAW.md).
2. **Violations do not cost the same.** Claiming they do would be visibly false, and an
   agent that senses the falseness starts ranking rules silently by its own criteria —
   which is worse than an explicit ranking. So here is the explicit one.

What separates the tiers is **reversibility**, not importance:

| Tier | A violation costs | Rules |
| :--- | :--- | :--- |
| **Irreversible / systemic** | Data that does not come back, a promise broken to a client, a system dead in flight | 0G · 10 (duration clause) · 22 · 23 · 26 · 30 |
| **Structural** | The architecture degrades — repairable, but expensive | 0A · 0B · 0D · 0E · 19 · 20 · 21 · 25 · 27 · 32 · 33 |
| **Convention** | A rename, a reformat, a rewritten commit message | 0 · 1 · 2 · 14 · 15 |

**Two situations where this matters, and only two:**

* **Two rules collide.** The higher tier wins, and **the arbitration is written down** — a
  genuine collision usually means one of the two rules is badly worded and needs fixing.
* **Time pressure forces a trade-off.** A convention can wait for the next commit. An
  irreversible rule never waits, and "we were in a hurry" is not a reason that exists here.

Outside those two cases, the tiers change nothing: you comply with all of them.

---

<a id="rule-0-language-collaboration-protocol"></a>

## Current construction scope

This is the complete local V1.15 rulebook. [The self-contained adoption decision](decisions/2026-10-06-SELF-CONTAINED-CORPUS.md) and the [6 October construction and execution direction](decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md) govern the present scope. Implementation artifacts named below are produced in the separate realization, not supplied by this code-free OS. The constructor generates missing code and precise contracts; only a genuinely undecided authority/business policy blocks its dependent action. A protection boundary is not a CLI permission prompt: authorized DEV executes fully, and production applies the tandem's verified per-action/type rights.

<a id="rule-0"></a>
### Rule 0: Language & Collaboration Protocol (Total Invariant)
* **English for All Technical Assets**: 100% of source code, variable/function names, API schemas, JSON payloads, Git commit messages, branch names, technical specifications, and repository documentation (`README.md`, `RULES.md`, `ctx-universe.md`) MUST be written strictly in **English**.
* **French for Human-Agent Pair Programming**: All strategic discussions, planning sessions, architectural reflections, live brainstormings, and human interactions are conducted fluently in **French**.
* **Zero Mixing Enforcement**: Never write French comments, docstrings, or technical documentation in code repositories. Never respond to the human operator in English unless quoting an exact external error or artifact.

---

<a id="rule-0a"></a>
### Rule 0A: Three Perimeters Taxonomy (P1 / P2 / P3)

Every component, package, brick, or app MUST be classified into **exactly one** perimeter before design or deploy. Canonical source: [perimeter taxonomy](docs/architecture/PERIMETERS.md).

| Perimeter | Objective | Examples |
| :--- | :--- | :--- |
| **P1 — Minimal socle** | Secrets, audit, auth, generic jobs, boot — zero business logic, zero mandatory LLM | `@shaper/pkg-vault`, `@shaper/pkg-logger`, `@shaper/pkg-auth`, `@shaper/pkg-queue`, `@shaper/pkg-db` |
| **P2 — Agentic** | Deterministic beats, bridges, Helm and the assistant organism behind it | `@shaper/pkg-maestro`, `@shaper/pkg-mail-agent`, bridges, `brick-helm`, `@shaper/pkg-ged-engine`, `@shaper/pkg-rag` |
| **P3 — Business / client tools** | Persistent vertical apps **outside** P1+P2 — separate port, volume, lifecycle | `market-intelligence`, `enterprise-chat`, `univ-sinistre`, CRM POC |

* **Rule 0F alignment**: Helm is **P2**, whoever holds it: perimeter is the layer, never the owner, so a client pilot at the Helm does not make it P3. Client ERPs, scrapers and human-to-human business chat are **P3** — never merged into Helm.
* Helm voice STT/TTS and its `/console` interface remain P2. Compatibility routes, if provided, resolve to that one interface.

---

<a id="rule-0b"></a>
### Rule 0B: Universal Parametric Genericity Invariant (Zero Hardcoding)
* **Everything Behaves as a Parameterized Function**: Every script, engine, deployment workflow, container blueprint, and documentation guide MUST be engineered as a pure, parametric abstraction that receives its parameters via CLI arguments, environment variables, or configuration manifests.
* **Multi-Infrastructure Portability**: Implementations remain parameterized across supported profiles on Proxmox VE, LXD, raw KVM, standalone bare-metal Debian, or cloud VPS instances (Hetzner, OVH, Scaleway, AWS, home-lab) without environment-specific source edits; qualify the selected host profile rather than claiming every host has been tested.
* **Zero Hardcoded Environment Residue**: Never hardcode specific IP addresses, hypervisor node names, private subnets, tenant domains, or static credentials into code, scripts, or specifications.
<a id="rule-0b-intent-header-classification"></a>
* **Mandatory Intent Header Classification (Generic vs Specific)**: Every `INTENT.md` or blueprint document in SHAPER OS MUST declare its exact classification at the very top header:
  * `> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)` for reusable abstract bricks in `SHAPER-OS/`.
  * `> **Intent Classification**: SPECIFIC INTENT (Universe: <univ_slug>)` for concrete instantiated deployments in experimental sandboxes or apps.
* **Strict Distinction: Abstract Specs vs Concrete Examples**: Technical documentation must always define abstract parameterized interfaces first (e.g. `<CLIENT_MESH_IP>`, `<GATEWAY_HOST>`, `<DOMAIN_NAME>`).
* **Explicit Demarcation of Specialized Examples**: Following any generic documentation, specialized real-world implementation examples (e.g. a specific Proxmox hypervisor, cloud node, or demonstrator) MAY be provided, but MUST ALWAYS be explicitly labeled under a dedicated section header: `### Illustrative Example (Non-Binding / Demonstration Only)`. There must be zero ambiguity between universal contracts and specific illustrative cases.

---

<a id="rule-0c"></a>
### Rule 0C: Declarative Agent-First Simplicity

* Blueprints state intent, invariants, environment, runtime and security in plain English, normally four to six high-signal points, with detailed contracts where necessary. Brevity never removes an obligation or exact interface.
* This OS repository contains documentation only. Exact field names, protocol values, diagrams and configuration requirements are documentary contracts; implementation code and executable examples belong in a separate realization repository.
* The constructor generates implementation and host-specific recipes from the intent. No pre-existing code, image, registry or installer is needed to start.
* Runtime adaptation is parameterized and respects the declared boundaries. The human supplies live direction; the agent makes ordinary implementation choices within that mandate.
* Keep reusable intent concise and separate from a concrete example. A documented constraint does not promise infallible model behavior.

---

<a id="rule-0d"></a>
### Rule 0D: Dual Intent & Topology Manifest Protocol (INTENT.md + JSON)

SHAPER OS uses **two complementary layers** — never one replacing the other:

| Layer | File | Audience | Purpose |
| :--- | :--- | :--- | :--- |
| **Declarative Intent** | `INTENT.md` | Humans & AI agents | Philosophy, invariants, security boundaries, parameterized contract |
| **Topology Manifest** | `topology.json` (repo root) or local `deps.json` | Scripts, CI, agents, Quadlet tooling | Machine-readable dependency graph, boot order, ports, `requires` / `provides` |

* **INTENT.md is mandatory** for every `@shaper/*` package and every `brick-*` directory. It answers *What* and *Why*.
* **JSON manifests are mandatory at ecosystem level** via the canonical root `topology.json` generated in the realization repository. It answers *Who depends on Whom* and *In what order*.
* **Optional local `deps.json`** MAY exist inside a `packages/<name>/` or `bricks/brick-<name>/` directory when a component needs to declare overrides for a specific universe — but the root `topology.json` remains the master graph.
* **Zero duplication of philosophy in JSON**: JSON files MUST NOT repeat INTENT prose. They carry only structured fields: `id`, `type`, `requires`, `optional`, `provides`, `port`, `bootAfter`.
* **Agent-Synthesized Defaults**: Business rules and deploy details are **not** stored in `topology.json` unless a human explicitly requests an override. Silence = agent decides freely, as long as each brick `INTENT.md` invariants are respected.
* **Override Protocol**: When a human states a specific constraint (port, path, schema, dependency), add it to `topology.json` or a local `deps.json`. Never preemptively.
* **Validation**: Any `doctor`, bootstrap, or deploy script MUST read `topology.json` for ordering — never hardcode dependency chains in shell scripts. The constructor supplies graph validation against `topology.json` and actual imports, following the [topology contract](docs/architecture/TOPOLOGY.md).

---

<a id="rule-0e"></a>
### Rule 0E: Materialization Pipeline (Intent → Construction → Proof → Reuse)

The primary deployable unit is a `brick-<name>`: its intent and a Podman image. Extracting reusable source packages is optional and follows stabilization or a testing need.

| Step | Owner | Required result |
| :--- | :--- | :--- |
| Intent | Human–agent tandem | Objective, mandate, invariants and observable acceptance |
| Construction | Agent | Implementation, image build and entrypoint in a separate workspace; unresolved implementation details are its work |
| Proof | Agent and tandem | Native tests, the real unit alone, then integration with its actual peers; record independent effects and typed evidence |
| Freeze | Tandem | Immutable source revision and image digest in the realization lock; no floating `latest` in production |
| Deploy | Authorized realization tooling | Apply the declared topology and verify results |
| Reuse | Tandem | Recommend a registry when reusable artifacts exist; publish only within the mandate |

The intent constrains construction, tests prove a particular artifact, and the lock identifies the bytes. No pre-existing registry is a prerequisite. Generated automation reads the realization's topology; a package is a stabilization artifact, not a condition for first deployment.

---

<a id="rule-0f"></a>
### Rule 0F: Helm Is the One Human Interface to an Ecosystem; Business Tools Stay Distinct Applications

* **Helm is the conversational interface between a human and the ecosystem in
  their charge**: web and mobile web, text and voice. A pilot asks; Helm
  answers, prepares and, within authority, acts, over the universes of that
  pilot's jurisdiction and nothing else.
* **Two settings, and no third** (Rule 37): its **jurisdiction**, the universes
  it may see and act upon down to their constituent pods, and the
  **pilot level**, what the person at the Helm has validated. The master root and a
  client's jurisdiction root use the same Helm; what differs between them is
  the jurisdiction, never a second product.
* **Helm is never the authority**: it sends a requested operation to Runtime,
  which checks root and mandate, correlates the operation and writes the
  evidence . A structural change is materialised by a maker
  under the master root (Rule 36), never by Helm itself.
* **What a class does not offer becomes a proposal to the class**: a
  jurisdiction root at the shaping level adds, configures or removes what its
  classes offer. A feature no class offers becomes a change to the class, made
  by the class's makers, never an exception inside one instance (divergence is
  Rule 33's fork). A **blank universe** (a scoped offer: a universe
  granted without class content to an infrastructure client) is the one place
  where a jurisdiction root builds what it wants, bounded by its backup
  contract.
* **Client business tools are strictly distinct applications** (unchanged since
  the first reading): ERPs, vertical business portals, customer dashboards,
  human-to-human business chat (`enterprise-chat`), mini-apps and external
  widgets (e.g. `univ-sinistre`, `univ-immo`) are built, deployed and served as
  **standalone, distinct applications/containers**, with their own UX,
  authentication boundaries and branding. They never pollute, overload or merge
  into Helm; Helm and the agentic organism behind it (P2) are the engines and
  endpoints they consume.

---

<a id="rule-0g"></a>
### Rule 0G: Strict "NO FAKE, NO FALLBACK" Testing & Validation Invariant

* **Zero Simulation / Zero Mock in Integration Tests**:
  * Tests MUST NEVER simulate, fake, mock, or emulate real operations when validating system capabilities, container runtimes, APIs, or AI agent autonomy.
  * No mock servers, no synthetic HTTP stubs for core services, no dummy return values masquerading as real execution.
* **Real Environment Execution for Capability Proof**:
  * Every integration/capability test MUST hit the **real running services** (the real Vault AES encryption, the real Logger audit persistence, the real Queue and its private MariaDB, the real GED filesystem, the real Qdrant vector engine, the real Podman runtime).
  * If a command is tested (e.g. `podman run --rm alpine uname -a`), it MUST actually spin up the real container and return real kernel output.
* **Zero Silent Fallback / Fail Hard**:
  * Tests and test runners MUST NEVER silently swallow errors, fall back to simulated success, or catch exceptions just to output a green checkmark.
  * If a service or command fails, the test MUST fail hard, emit the exact raw error, and force a real architectural resolution.
* **Agent Self-Validation Contract**:
  * When the AI agent proves it can execute a task (e.g. configuring a mailbox in the Vault, querying the cluster, analyzing a document in `/data/ged/`), it must execute the real shell/API commands and verify the real state on disk / in memory. Fake results, invented numbers, or simulated completions are strictly forbidden.

---

Unit-test doubles may isolate a code path, but never substitute for real integration, deployment or action evidence.

<a id="rule-0h"></a>
### Rule 0H: Universal Interchangeable CLI Matrix & Human-Arbitrated Economics

* **Common Semantics across Qualified Adapters**:
  * SHAPER OS is strictly agnostic to the underlying AI agent CLI .
  * The system decouples the intelligence engine from the orchestration fabric via standard Bridge interfaces (`/api/conversations/*`, SSE streams). A replacement must implement the required declared capabilities; a missing capability is an adapter gap, not implicit equivalence.
* **No Engine Is Named In This Canon**:
  * A rule that names a model expires with that model. The authority on engine
    selection is [`docs/architecture/COGNITION.md`](docs/architecture/COGNITION.md): work declares the reasoning
    depth and throughput it requires, and the deployment measures which engines
    actually satisfy it **from the target host**.
  * Concrete engine names, versions and prices live in the **measured runtime
    matrix** produced at each deployment — never as a universal model requirement; a specific adapter profile declares its selected provider and execution mode. Published benchmarks are advisory; measured availability decides.
* **Human-Governed Economic & Mission Arbitration**:
  * The choice of engine belongs to the **human operator**, adjusted according to
    budget, privacy and task complexity. The arbitration is expressed in **classes**,
    which outlive the products that populate them:
    * **Class F — Free / default bootstrap**: reachable at zero cost, no paid key. The default for routine administration, tests and orchestration.
    * **Class L — Local / air-gapped**: runs entirely inside the perimeter. Throughput is traded for sovereignty; a cloud fallback from this class is a violation, not a convenience.
    * **Class P — Paid, balanced**: commercial engines for fast professional iteration.
    * **Class E — Paid, frontier**: the deepest reasoning available, for high-stakes work that justifies its cost.
    * **Class A — Aggregator**: multi-provider routing across several of the above.
  * A class is a budget and a privacy posture, not a brand. Mapping a class to a
    concrete engine is a deployment-time decision, recorded with the measurement
    that justified it.
* **Bridge Compatibility Invariant**:
  * Every CLI runtime connects to Helm and receives identical context digests (the universe context file, `topology.json`, persistent memory).

---

The common [cognition-bridge intent](docs/intents/cognition-bridge.md) owns session, context, ledger and execution semantics. OpenCode is the selected reference composition, not universal provider law.

<a id="rule-0i"></a>
### Rule 0I: Pure IA-Driven Installation Doctrine (Zero Installer Monoliths / Pure Intent Synthesis)

* **Zero Rigid Installation Programs ("No Hardcoded Installers")**:
  * SHAPER OS strictly forbids writing monolithic, rigid installation programs, closed binaries, or brittle procedural shell wizards that assume fixed paths, hypervisor quirks, or rigid hardware layouts.
* **Everything Starts from Declarative INTENT**:
  * The human or architect declares the **INTENT** (`INTENT.md`, `topology.json`, security boundaries, required invariants).
* **The AI Agent Directly Fabricates and Shapes the Socle**:
  * Installation is a 100% **IA-Driven Process**: the autonomous AI agent  reads the declarative intent, probes the physical host and runtime limits (`cgroups`, RAM, disk, kernel version, existing packages), and **synthesizes, provisions, and configures the environment on the fly**.
* **Dynamic Synthesis Over Fragile Scripts**:
  * If a dependency is missing, the AI agent resolves and installs the exact right package for that specific OS runtime (`apt`, `apk`, `pip`, `npm`).
  * If an environment configuration or port needs adjustment, the AI agent adapts dynamically within the declared parameters and mandate. Apply [Rule 11's port-conflict contract](#rule-11-declared-ports-are-free): identify the holder and record the resolution; do not silently substitute a declared port or stop an unrelated service. Ordinary choices already covered by the mandate require no repeated approval.
  * **Summary**: The human sets the *What* and the *Why* (Intent); the AI agent dynamically constructs and validates the *How* (Materialization).

---

<a id="rule-0j"></a>
### Rule 0J: Human–Agent Construction and Required Secrets

* The human directs the project and mandate; the agent realizes it and exposes material decision gaps.
* Before an operation that needs a credential, check that its declared secret reference resolves to a nonempty, appropriate credential through the authorized secret channel. Never start a dependent operation hoping an absent secret works or supplying a dummy value.
<a id="rule-0j-zero-blind-execution"></a>
* A genuinely missing credential blocks its dependent operation. State the missing capability and how the operator can provision it securely; continue independent authorized construction. Do not require unrelated production credentials for a local build, or ask for a secret already available through an authorized channel.
* Keep runtime credentials consistent with their declared consumer and deployment. Propagate only the references and secrets that unit is entitled to use; never copy a universe's entire secret set into every container.
* A complete configuration enables repeatable construction and qualification; it does not constitute evidence that an untested implementation succeeds. Experimental partial configurations must identify inactive or degraded functions rather than presenting them as qualified.
* Use the declared DEV execution mode and production action policy in the [common bridge contract](docs/intents/cognition-bridge.md). Security design begins with construction; dedicated hardening follows integrated functional acceptance.

---

<a id="rule-0k"></a>
### Rule 0K: Channel Authentication, Explicit Outcomes and Session Rebirth

* A configured channel credential replaces stale consumer configuration. Its caller and receiver must agree on authentication for `/reset`, `/clear`, `/stop` and `/inject`; tokens may be scoped per channel. Do not require one shared all-powerful token across Helm, Bridge, Queue and Maestro.
* A terminal or idle bridge event must yield a visible final outcome. Surface tool aborts, timeouts and errors explicitly. If there is no text result, produce an honest status summary, never fabricated completion; the interface and voice surface must not hang silently.
* Reborn clears the requested conversation and local timeline, immediately loads the current authorized Presentation Briefing and context, and retains the returned Prime run in the UI. It does not erase business records, completed-action evidence or unresolved effects. Reconcile those before further action.
* Changes to a pipeline require its own closed-loop test: unit tests prove parts, the loop proves their interaction. That test belongs to the owning realization; generate it when absent. A simulated loop cannot qualify real bridge, voice or business execution.
* Conversation history, current context and the owning unit's durable action ledger have distinct roles; apply the [common continuity contract](docs/intents/cognition-bridge.md).

---

<a id="rule-1"></a>
### Rule 1: Canonical Naming Conventions & the Universe Repo Grammar

* **The universe class repo grammar**: `univ-<projet>-<classe>`, where
  **projet is ONE word, no hyphen** — everything after the first word is the
  class, which may be composite. One-line parse:
  `^univ-[a-z0-9]+(-[a-z0-9]+)+$`. A single-class project takes `-core`
  (`univ-mailo-core`): five characters against a future rename, settled.
* **The five repo kinds, exhaustively** — every git repository in the
  ecosystem is exactly one of these, and nothing else exists:

| Kind | Naming | Example |
| :--- | :--- | :--- |
| The base | `SHAPER-OS` (versioned folder/repo) | `shaper-os-v1.15` |
| The catalogue | `SHAPER-OS-BRICKS` | `<catalogue-repository>` |
| A universe class | `univ-<projet>-<classe>` | `univ-boutik-shop` |
| A fork's catalogue | `<projet>-bricks` (Rule 33 forks only) | `fortex-bricks` |
| The fleet map | `<scope>-fleet` | `shaper-fleet`, `fortex-fleet` |

* **A release is an independently readable slice**: its full governing documentation lives in its own repository; implementation releases live in their separate realization repositories. Fleet records pin repository and immutable tag. Independent releases may run side by side; changes are deliberately carried and qualified, never presumed inherited. Verify the destination remote before the first authorized push of a copied workspace.

* **The mirror rule (Rule 33 forks)**: a fork swaps **only the projet word**
  and keeps every classe word, repo kind and file name verbatim
  (`univ-boutik-shop → univ-fortex-shop`). A fork costs zero new vocabulary,
  and `shaper verify` can hold it via the repo-level `forkedFrom`.
* **Classes have repos; instances never do.** An instance is a ledger row +
  a vault + volumes. Runtime instance names follow the triumvirate lifecycle
  (`<slug>-dev`, `<slug>-test`, `<slug>-prod`, Rule 36); DNS names are declared by the realization and remain unique within its domain.
* **Package and brick prefixes are unchanged**:

| Element Type | Scope / Layer | Canonical Naming Convention | Real-World Examples |
| :--- | :--- | :--- | :--- |
| Composable Logic Bricks | NPM Scope `@shaper/` | `@shaper/<brick>` | `@shaper/pkg-vault`, `@shaper/pkg-logger`, `@shaper/pkg-queue` (**P1**); `@shaper/pkg-maestro`, `@shaper/pkg-mail-agent`, bridges (**P2**) |
| Deployable bricks | OCI images | `brick-<name>` / `img-<name>` | `brick-vault`, `brick-forge`, `img-logger` |

* **Brick Isolation Invariant**: A `@shaper/*` package never has knowledge of the universe consuming it (zero coupling, 100% isolated unit test coverage).
* **The meta-rule this grammar serves**: *the identifier says WHAT a thing is;
  structured data (manifest, LINEAGE.md, ledger row, fleet.yml) says where it
  comes from and where it sits.* No slug ever encodes graph position,
  perimeter, or lineage — those live in data, so the graph can evolve without
  a rename (see Rule 37).

---

<a id="rule-2"></a>
### Rule 2: Atomic Git Changes with Declared Authorship

* The human is the Git author. A materially writing agent is identified in a truthful `Co-Authored-By: <agent identity> <email>` trailer; an advising or reviewing agent uses `Agent-Assisted-By: <agent identity> <email>`. State the actual engine/version when known and do not invent one behind an alias.
* A wholly human change declares `No-Agent-Assistance: true`; that marker is mutually exclusive with agent attribution. Multiple actual contributors may be identified.
* Keep changes atomic by component or coherent feature, with an English description and a clean, verifiable history. Commit and publish within the human's mandate; preparing an atomic change does not override a request to wait for review.
* The realization verifies missing or malformed attribution and incompatible markers. This documentation does not claim that an executable provenance guard ships here.
* Attribution records who produced the change so that later defects can be traced to a decision or derivation.

---

<a id="rule-3"></a>
### Rule 3: Podman Images and Service Management

When software or configuration affects a container, rebuild the image, record its immutable digest, apply the authorized service-manager update and verify the actual service. The realization declares its Quadlet/systemd configuration or equivalent compliant service contract.

Build locally for the first construction. A registry is recommended for repeated distribution once reusable images exist, and its address is an operator parameter reachable from inside the consuming universe. Never invent a registry address or make an existing registry a bootstrap dependency. Production consumes the locked artifact, not a floating tag.

---

<a id="rule-4"></a>
### Rule 4: Standard Application Layout & Per-Functional-Podman Database Isolation
* **Standard Application File Structure (`/apps/<slug>/`)**: Every deployed application or service brick adheres strictly to the canonical application filesystem hierarchy — **same spirit under Podman**: persist what must survive in bind-mounted volumes, never mix cache with backups:
  ```
  /apps/<slug>/          # or <univ>/ for a Podman universe
  ├── app/               # Code (git) — not a substitute for volume backup
  ├── etc/mysql/localhost/passwd
  ├── log/               # Append-only JSONL
  ├── sav/               # Persistent volumes (bind-mounted into Podman) — MUST be backed up
  └── nosav/             # Cache, node_modules, image layers, bulky regenerable files — EXCLUDED from backups
  ```
* **Mandatory Functional-Podman Database Convention**:
  * **Every Functional Podman Owns One**: Every application, telephony, agent,
    queue, logger, vault or other functional Podman materialises its own MariaDB
    instance inside that Podman's security and lifecycle boundary. A universe
    therefore contains as many independent MariaDB instances as functional Podmans.
  * **Never Shared**: No universe-wide MariaDB exists. A Podman never reads or
    writes another Podman's database, even inside the same universe, and no parent,
    child or peer universe crosses that boundary.
  * **One Name Everywhere**: the functional slug is the function identity, the
    Linux system account, the MariaDB account and the MariaDB database name:
    `<functional-slug> = system-user = database-user = database`. The Podman
    container may retain its canonical prefixed runtime name; that runtime name
    does not replace or alter the functional identity. No alias and no default
    credential may break this equality.
  * **Private and Self-Contained**: The database is reachable only from its owning
    Podman's function. Its volume, credentials, migrations, backup and restore proof
    travel with that function's contract.
  * **Separate Application and Administrative Paths**: the application process
    runs as `<functional-slug>` and connects only as the matching MariaDB user to
    the matching database. An authorised creation, development or operations agent
    administers MariaDB through the local `root` command-line path and has the
    database privileges required by its mandate. The agent never administers the
    server with the application's login or password; the application never receives
    the MariaDB root credential. Root authority does not widen the agent's universe
    mandate or permit cross-function data use.
  * **Password Resolution Order**:
    1. Primary source of truth: read directly from
       `/apps/<functional-slug>/etc/mysql/localhost/passwd`. It contains the
       generated MariaDB password, is mode `0600`, belongs to the functional
       system account, and is never committed, logged or baked into an image.
    2. Fallback (disposable Dev / CI only): read from
       `process.env.MYSQL_PASSWORD`. This fallback never qualifies an artefact
       for test, demo or production promotion.
  * **Born With the Function**: MariaDB and the four-way identity above are
    materialised when the functional Podman is born, even before the function
    has durable rows. SQLite, CSV and JSONL may be declared as disposable DEV
    scaffolding only; they never satisfy the database or promotion gate.
* **Continuous Architectural Traceability**: Document every architectural choice with *What* (concise description) and *Why* (business rationale).

---

<a id="rule-5"></a>
### Rule 5: Native Unit and Contract Tests
* A 100% pass rate for the complete applicable native/unit and contract suite is required before staging or production promotion. Generate meaningful tests for the selected implementation.
* Use the selected language's native test facilities and avoid unnecessary heavyweight frameworks. In a Node.js realization, the native runner is `node --test` and the cold test-process startup budget is 2000 ms; measure that scoped test budget rather than presenting it as a universe boot or recovery promise.
* The OS does not require every implementation to use Node.js. Language choice remains subject to the agnostic construction direction and the owning unit's actual contract.

---

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
  [operating contract](docs/agent/OPERATING-CONTRACT.md#decision-hygiene-qualification)
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
    ([`docs/architecture/COGNITION.md`](docs/architecture/COGNITION.md)).
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

A cognition bridge additionally obeys [bridge status](docs/contracts/bridge-status.md) and the [common session/context/action contract](docs/intents/cognition-bridge.md). An endpoint's health never proves model execution, permission or the task's external effect. Provider-specific transport mappings belong in the selected adapter's concrete contract.

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

Security is designed from the outset; implement functional/perimeter necessities while the tandem directs DEV. After integrated functional acceptance, finalize and enforce the designed production roles, jurisdictions and per-action/type rights, and replay accepted workflows under them before promotion. See [lifecycle](docs/agent/LIFECYCLE.md).

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
* A service start recreates the complete application container from its known image. Its declared non-reproducible volumes survive. A class may add bricks but may not invent an in-place patch as a fifth recovery operation. The [consulted-context doctrine](docs/design/CONSULTED-CONTEXT.md) explains the design/acting boundary.
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

<a id="rule-23"></a>
### Rule 23: External Healing Law (Parent Repairs Child)
* **Zero Self-Destructive In-Flight Modification**:
  * An AI agent NEVER modifies its own active infrastructure files, its bridge server, or its running process during execution .
  * Any structural repair, recovery, or update on an Agent of Level $K$ is MANDATORILY performed by the Parent Supervisor Agent of Level $K+1$ (or by the human operator) operating out-of-band at cold boot.

---

<a id="rule-24"></a>
### Rule 24: Root Guardian Law (Sentinel / Human Repairs Root)
* **Out-of-Band Root Supervision**:
  * For the Root Universe of a fractal tree (Level $N$, with no parent in the tree), integrity monitoring and emergency patching are performed by a **Sentinel Sidecar Agent** or by the **Human Operator using an external IDE (Cursor, Antigravity, Claude Code)** via an isolated control channel.
* **The root universe is the master root's** : the tree has one top, held by the **master root** of Rule 37 — the founding tandem of a human Steward and the root agent under their direct control, root from underneath every host (Rule 36). Its own universes carry the governor and the makers, which take direction from it alone. It grants every jurisdiction. A **jurisdiction root** holds full power inside what it was granted, down to the pods of its universes, yet it is never the root universe of this rule: it sits under a parent, reaches no host, and is repaired from above like any child (Rule 23).

---

<a id="rule-25"></a>
### Rule 25: Canary Deployment & Downward Rollback (Anti-Propagation)
* **Progressive Fleet Updates**:
  * Whenever a Parent Universe distributes a configuration or brick update to its child fleet:
    1. **Canary (1/N)**: Deploy to 1 pilot child universe only.
    2. **Observation Period**: Monitor logs and health for $T$ minutes (bake time, default 5 min).
    3. **Phased Rollout**: If the canary passes its gate → deploy to 10%, then 100% of the fleet.
    4. **Automatic Rollback**: At the first failure on the canary, immediately roll back without touching the rest of the fleet.
* **The Canary Gate Is the Typed Gate (R20), Not the Health Port**:
  * A `200 OK` on `/api/health` is a liveness signal, never a validation signal. A canary is declared green only when it has produced at least one real deliverable of its universe's nominal type **and that deliverable passed its Rule 20 typed verification contract**.
  * Bake time without a produced-and-verified deliverable does not count as green: the rollout stops and escalates rather than proceeding blind.

---

<a id="rule-26"></a>
### Rule 26: Complete Database Isolation (MariaDB per Functional Podman)
* **Zero Domino Effect on Data**:
  * To guarantee total blast-radius isolation, each functional Podman operates
    its own MariaDB instance inside its own security, storage and lifecycle
    boundary. There is no shared database at universe level.
  * Asterisk, Helm, Vault, Logger, Queue and every other functional Podman each
    own a different MariaDB instance and credentials. A failure, migration or
    compromise of one database must not reach another function.
  * A functional Podman's birth and qualification fail when its MariaDB is
    absent, unhealthy, reachable outside its boundary, non-persistent, or lacks
    a successful restore proof. CSV, JSONL, SQLite or another Podman's database
    cannot substitute for this gate.
  * Qualification also fails unless the running function uses the Linux account
    named by its functional slug, its MariaDB account and database use that same
    slug, the password is read from
    `/apps/<functional-slug>/etc/mysql/localhost/passwd` with mode `0600`, and
    credentials belonging to another functional Podman are refused.
  * Database administration proof uses the local MariaDB root CLI path; application
    behavior proof uses only the confined functional account. Passing one path does
    not prove the other.
  * **Legacy transition**: an already-running instance that predates this
    invariant may continue unchanged while it remains serviceable; its existing
    SQLite, CSV or JSONL store is recorded as technical debt, not presented as
    compliance. No forced in-place migration is implied. The gate becomes
    mandatory when that functional Podman is rebuilt, replaced, rematerialised
    or promoted: the new artefact must carry its private MariaDB and pass the
    complete qualification above before it takes over.
  * The Central SaaS database holds exclusively the node inventory registry and global billing data.

---

<a id="rule-27"></a>
### Rule 27: Reconciliation Convergence Guard (Anti-Flapping & Resting Degraded State)
* **A Reconciliation Loop That Cannot Give Up Is a Storm Generator**: The owning reconciliation engine, which may be triggered by Maestro (desired manifest ↔ observed state persisted in its private database) MUST bound its own corrective action.
  * **Exponential Backoff**: Repair attempts on the same drift signature back off (e.g. 30s → 1m → 2m → 4m), never retry at fixed beat cadence.
  * **Bounded Attempts**: The realization declares a finite `maxHealingAttempts`; when none is supplied, the default is 5. After that configured number of attempts on the same drift signature, the supervisor STOPS attempting repair.
  * **Resting `DEGRADED` State**: The child universe is marked `DEGRADED` in the parent registry, its drift signature and last diagnostic are recorded, and the human operator is alerted. `DEGRADED` is a resting state, not a retry state — it never self-clears. Its authorized exits are specified below; `REAPED` is the terminal lifecycle state.
  * **How a `DEGRADED` row is left** : a DEGRADED row leaves that state by its account's explicit new ask, for the environments a robot may end (`dev`, `test`, `demo`) — the broken row's deadline becomes now, a maker reaps whatever half-exists and reports `REAPED`, and a fresh row is born beside it; the broken one was a failure the account was stuck behind, not a life to protect. A **`prod`** row leaves it only by human or Root Guardian action: a robot's re-ask is refused as a typed fact carrying the row id, no twin is born, and the reap recipe refuses to end a production universe (exit 4, reported `REAP_REFUSED` — a fact, not a failure) so that the row rests and the alarm leaves out of band. The same bounds apply to the governor's own offers: a reap that failed is offered again under exponential backoff and never beyond `maxHealingAttempts`; a reap that was refused is never offered again.
  * **Fleet-Wide Circuit Breaker**: If more than 20% of a fleet enters `DEGRADED` within one bake window, the parent suspends ALL reconciliation and rollout activity on that fleet and escalates. A systemic fault must never be amplified N times.
* **The Escalation Channel Is Declared, Never Assumed**: "Alert the operator" is meaningless until the channel exists. Each universe declares its `alerting` channel in `manifest.json` — mobile push, mail, Telegram, or an existing prod-alerting relay. The channel depends on what is being watched and is decided case by case; the doctrine imposes only the contract:
  * It reaches a **human out-of-band** — never a UI nobody is looking at.
  * It is **tested at deploy time** like any other brick: an unverified alert path is an absent alert path (Rule 0G).
  * A universe with no declared channel MUST NOT be promoted beyond DEV.
* **Rationale**: Without these bounds, one invalid manifest on a 50-child fleet produces 50 simultaneous restart loops — the reconciliation engine becomes the outage.

---

<a id="rule-28"></a>
### Rule 28: Sovereign WAF Rule Validation (No Unproven Guardian)
* **An AI-Generated Allow-List Is a Hypothesis, Not a Defence**: The sovereign WAF/aiguilleur allow-list is synthesized by the parent agent that knows the application's legitimate routes. It is therefore an artefact like any other and falls under Rule 20.
  * **Mandatory Attack Corpus**: Before any WAF ruleset reaches production, it MUST pass a versioned attack corpus stored in the repository — at minimum: SQLi, XSS, path traversal (`../`), verb violation on a `GET`-only route, and rate-limit saturation.
  * **Mandatory Legitimate Corpus**: The same ruleset MUST let through a versioned corpus of legitimate business requests. A WAF that blocks real customers is an outage, not a protection.
  * **No Silent Rule Drift**: Any regeneration of the allow-list re-runs both corpora and is deployed to the fleet under Rule 25 (canary first).
* **Scope Discipline**: The sovereign layer's uncontested role is **routing** (routing universe → container) and **precomputed cache serving**. Generic attack signature filtering SHOULD delegate to a maintained engine (OWASP CRS via Coraza / ModSecurity) rather than being reimplemented; the doctrine forbids presenting a hand-rolled signature filter as equivalent protection.

---

<a id="rule-29"></a>
### Rule 29: Constructive Integrity (Every Fixed Bug Becomes a Test)
* **The System Grows a Memory of Its Own Failures**: Any resolved defect — in code, in a manifest, in a WAF rule, in an agent prompt — MANDATORILY gives birth to a new non-regression test committed alongside the fix.
* **No Fix Without Proof**: A patch whose accompanying test would still pass on the unpatched code does not demonstrate anything and is rejected.
* **A Correction Lives Where It Survives**: A defect met while deploying or operating a universe is corrected in the **generic path** — the brick, the package, the template, the example deploy script — never only in the universe where it appeared. Its test is placed where it will still run after that universe is gone.
  * **Why this is a rule and not advice**: a `-test` universe is destroyed by Rule 10, and a `-dev` one is disposable by design. A fix written into an instance is deleted with the instance, and the next clean sheet meets the same wall having learnt nothing. The next clean construction must inherit the correction from its owning source and test.
  * **The test decides where the fix belongs**: if the non-regression test would disappear with a universe, the fix is in the wrong place. Move both.
  * **A universe may still specialise**: this forbids *correcting* in an instance, not *parameterising* one. When a defect is genuinely specific to one deployment, say so in that universe's INTENT and explain why the generic path is right as it stands.
* **Antifragility Contract**: This is what makes the fractal tree antifragile rather than merely resilient — each incident permanently raises the floor for every universe instantiated afterwards. That floor only rises where the correction outlives the universe that found it.

---

<a id="rule-30"></a>
### Rule 30: Snapshot Before Migration (Data-Bearing Changes Are Not Canary-able)
* **Why This Rule Is Separate from Rule 25**: The canary protects against a bad configuration, because a configuration can be rolled back. A database migration **carries data**: rolling back the code does not bring back a dropped column. Progressive rollout is necessary here but not sufficient.
* **The Non-Negotiable Sequence**:
  1. **Full snapshot first** — the owning functional Podman's MariaDB dump plus its persistent volumes, taken immediately before the change, never a nightly backup "close enough".
  2. **Verified restore** — the snapshot is restored into an ephemeral sandbox and proven loadable. An unverified backup is not a backup (Rule 0G).
  3. **Only then** apply the migration, canary first per Rule 25.
  4. **Rollback = restore the snapshot**, not "run the reverse script".
* **Preferred Refinement (Expand / Contract)**: where feasible, make the change non-destructive in stages — add the new column, write to both, migrate readers, and only drop the old column in a later release once every universe in the fleet is confirmed migrated. Destructive and reversible steps never travel in the same deployment.
* **Fleet Scope**: a schema change affecting N functional Podmans is N independent migrations, each with its own snapshot. One shared migration transaction across functions or the fleet is forbidden — it would recreate the common point of failure Rule 26 exists to remove.

---

<a id="rule-31"></a>
### Rule 31: Declared Data Lifecycle (Per Universe, Not a Universal Policy)
* **The Doctrine Forces the Declaration, Not the Policy**: retention and erasure requirements depend entirely on the client and the use case. A personal mailbox and a client business database can need different policies; each declares the policy appropriate to its data and mandate. Imposing a single global policy would be wrong in both directions.
* **Every Universe Declares Its `dataLifecycle` in `manifest.json`**, with at minimum:
  * `personalData`: `true` / `false` — does this universe hold data about identifiable people?
  * `retention`: duration or `unlimited`, per data class (GED documents, JSONL logs, vector collections, database rows).
  * `onTermination`: what is destroyed, what is exported to the client, and in what format, when the universe is decommissioned.
* **`personalData: false` Is a Valid and Common Answer** — but it must be written down, not left silent. Silence is not a declaration.
* **Erasure Is Fractal**: deleting a client's data means deleting it in every store of that universe — MariaDB rows, `sav/` volumes, GED files, **and its Qdrant collection**. A vector left behind is a leak; the isolation of Rule 22 is what makes this deletion tractable in the first place.

---

<a id="rule-32"></a>
### Rule 32: The Perfected Generic Base Comes Before Any Specialisation (Founding Method)
* **How work is framed here, and it is not negotiable**: for each thing we build, we first **delimit a perimeter**, then we make what sits inside it **excellent, generic, extensible and open to what comes next** — a base that will interact with other systems we have not met yet. Business specifics are built *on top of it*, never *into it*.
* **Why it is the founding logic, not a preference**: this is what makes the four promised properties true rather than claimed. A base that is perfected once is **adaptable** (bricks swap instead of being rebuilt), **scalable** (behaviour does not change with volume), **alive** (it improves without a new project), and **multidimensional** (several things advance in parallel). And it is what makes the architecture genuinely **fractal**: the pattern is only worth repeating if the pattern is good.
* **The economic argument is explicit**: time spent perfecting the base is not time lost, it is time bought back on every project that follows. A specific requirement then costs an adaptation, not a rebuild — and often costs nothing at all because the base already covers it.
* **Binding consequences**:
  1. **No client requirement is ever written into a generic brick.** It goes into a P3 application or a declared handler. A brick that carries one client's particularity has stopped being a base.
  2. **A base is finished when it is boring** — when the next specific need is met by configuration and a handler, not by editing it.
  3. **Elasticity is part of "generic"**: the same brick must run modestly on a small VPS and hold up on a large server, by parameter and never by fork. A brick that only works at one scale is not a base.
  4. **When a specialisation forces a change to the base**, that change must be made *generic* before being merged — the particular case reveals a missing capability, it does not authorise a special case.
* **Applies to every agent working on this repository.** Delivering a working specific feature by contaminating a generic brick is a regression, not a delivery, however green the tests are.
* **The total vision is what dictates the steps on the base bricks.** A brick is never perfected in the abstract, against an imagined future — it is perfected **against the whole picture of where the project is going**. Holding the complete vision is what tells us which capability the base must carry, which one it must not, and in what order to build them. This is why the doctrine is written before the code: not as ceremony, but because the map is what turns "make it generic" into a list of concrete steps. An agent that has not read the vision cannot decide what belongs in a base.
* **A stray specific bit is not a catastrophe.** If something slightly specific slips into a brick, the sky does not fall: the day a *more* specific need arrives, we meet that same code again and generalise it then. What must hold is that **the broad lines cover a good part of the perimeter** — enough that we can walk into a client situation and discover the rest from a working base, not from nothing. Perfectionism that blocks delivery is not this rule.
* **The level of exigence is set per thing and per moment.** Not everything deserves the same rigour at the same time, and pretending otherwise stalls the work. Each brick is made robust *at its own level of exigence*, decided by the human. The declared requirement for the current component and stage governs.
* **Why full conformity matters where it does**: it is what guarantees that the bases we already have are conform, functional, and **deploy at will**. Conformity is not decoration, it is what makes redeployment boring.
* **Current sequencing**: security boundaries and necessary functional protections are designed and implemented during DEV. After the tandem accepts integrated functions, perform dedicated hardening using the complete view and verify the accepted paths under production permissions. Decisions about data governance, economics and any use-case constraints remain explicit tandem-owned declarations; no unseen doctrine page is a prerequisite.

---


Security boundaries are designed during DEV and necessary functional protections are implemented then. Detailed production hardening follows integrated acceptance, as specified in [Lifecycle](docs/agent/LIFECYCLE.md); it is not waived by generic-first construction.

<a id="rule-33"></a>
### Rule 33: The Client Fractal Fork (Assumed Divergence, Never Contamination)
* **The mechanism**: when a client's needs require it, we take the base bricks and **fork the whole solution fractally** for that client. The fork diverges from the original creation, and **that divergence is assumed** — it is the fruit of shaping something for a real need, not an accident to be repaired.
* **Why this does not contradict Rule 32**: Rule 32 forbids putting a client's particularity **inside a shared generic brick**. Rule 33 authorises **a separate branch of the tree** for that client. The base stays clean for everyone; the client gets exactly what they need. This is precisely what the fractal architecture exists to make possible — a branch has the shape of the tree without being the tree.
* **When to fork, and when not to**:
  * **Do not fork** for a small business need. An artisan's CRM is met with base bricks, a P3 application and declared handlers. Forking there would be paying a permanent cost for a temporary difference.
  * **Fork** when a client imposes requirements that reach into the socle itself — strict security posture, role systems, information compartmentation, regulatory constraints. Those cannot live as a configuration flag on everyone else's base.
* **Obligations of a fork**:
  1. It states **what it diverged from** — the base version it was cut at — and **why**. A fork whose origin is unknown cannot be maintained.
  2. It stays inside the law: forking the solution never means abandoning `RULES.md`.
  3. **A generic improvement discovered in a fork travels back to the base.** The particular case revealed a missing capability (Rule 32); the fork keeps its particularity, the base gains the capability.
* **Security follows the construction lifecycle**: design boundaries and implement necessary functional protections during DEV; finalize and enforce tailored production rights after integrated acceptance. Client-specific requirements may justify a fork, but every production realization has an explicit tandem-owned action policy.

---

<a id="rule-34"></a>
### Rule 34: A Bridge Ships Everything Its CLI Needs (Prerequisites Are Declared, Pinned and Proven)

A CLI bridge exists to run a command-line agent; a declared API adapter states its equivalent runtime dependencies. A bridge whose CLI **cannot start** answers `ok` on `/api/health` and does nothing — the most expensive failure shape there is, because everything downstream believes it.

* **The image carries the prerequisites, not the operator's memory.** Every runtime dependency of the CLI — interpreter, shell, fonts, language data, system libraries — belongs in the brick's image and is **pinned**. If a CLI needs something absent, it is the brick's duty to install it, declared in its `INTENT.md`. An operator who must remember to install something by hand has been handed a landmine.

* **A prerequisite is proven, never assumed.** The brick's health must establish that the CLI is **executable**, by running its own version command, not that a path was configured. `which` proves a string; running proves a binary. An image that only builds or only runs on some machines is not an artefact you can tag (Rule 0E).

* **Three traps that cost a session each, and are now law:**
  1. **Never mount a symlink into a container.** It arrives pointing at a path that does not exist there. Mount the resolved target.
  2. **Never mount a launcher without its siblings.** Modern CLIs ship as a small script that executes files beside it; mount the whole version directory or nothing.
  3. **Never assume the base image has a shell.** A launcher beginning `#!/usr/bin/env bash` fails on Alpine with `can't execute 'bash'`, and the exit code will not say so plainly.

* **A CLI may be bound to its host**: when qualification establishes that it cannot run in the unit container, declare a host-resident adapter and its address and evidence. This exception concerns the CLI adapter location, not the universe containment or per-unit database contract.

* **What a bridge must publish about its CLI**: the binary it resolved, the version it obtained by running it, and whether authentication is present. any test-only `stubMode` must be visible and must never be the live default — a simulated bridge that looks live is a lie with a long fuse.


---

<a id="rule-35"></a>

The adapter declares its actual noninteractive approval/sandbox modes. Mandated DEV uses full execution without CLI sandbox or repeated approvals. Production executes the exact authorized action envelope. A capability gap is reported and the constructor may implement a correct adapter; it is not a prohibition on construction.

### Rule 35: Experience Corrects the Intent, Not Only the Code (Constructive Integrity, Upstream)

Rule 29 requires that every bug resolved gives birth to a regression test. That protects the code. It does not protect the **next universe**, which is built from `INTENT.md` and not from our test suite.

* **A problem experienced updates the brick's `INTENT.md`.** Not a changelog of incidents — the *invariant the incident revealed*, stated as the brick's intent so anyone materialising it again starts from what we learned. A fix that lives only in code is a lesson one refactor away from being lost.

* **Write the constraint, not the anecdote.** "A missing CLI is a state, not a crash" belongs in the intent. "On 23 August the cursor bridge died" does not; it belongs in the commit that fixed it.

* **The test proves it today, the intent carries it forward.** Both are required, and they are not substitutes: a test constrains this implementation, an intent constrains every future one.

* **When a rule and the code disagree, the code is what changes** — unless the rule itself was found wrong, in which case it is amended deliberately, never quietly softened to match what was built (see `the realization’s recorded contract gaps`).

---

<a id="rule-36"></a>
### Rule 36: Fractal SSH Authority & Ephemeral Sandbox Access Law (Clean-Sheet Dev/Test Promotion)

* **Parent Authority Over Child Lifecycle**: To supervise, develop, and test improvements on a child universe without risking production, the Parent Universe ($K+1$) has the explicit authority to instantiate, access, and destroy child environments ($K$). An agent never mutates its own vital organs in-flight (Rule 23); its supervisor operates the lifecycle.
* **Cryptographic SSH Asymmetry**:
  * The Parent generates an **Ed25519 SSH authority key pair** stored in its Vault or `sav/ssh/id_ed25519`. The private key **never** leaves the Parent.
  * When an ephemeral child container is provisioned, the bootstrap mechanism automatically appends the Parent's public key (`id_ed25519.pub`) into `/root/.ssh/authorized_keys`.
* **Dynamic Suffix & Environment Separation**:
  * **`*-prod` (Nominal)**: Permanent production universe, dedicated port base (e.g. `9200`), persistent encrypted `sav/`, production DNS/tunnel (`app.example.com`).
  * **`*-dev` (Ephemeral Dev)**: Separate environment for active coding and prompt tuning, offset port base (e.g. `9300`), scratch storage, dev DNS/tunnel (`app-dev.example.com`).
  * **`*-test` (Clean-Sheet Validation)**: Rebuilt **from scratch** on a blank container to eliminate caching artifacts. Runs 100% unit tests + Rule 29 regression test + Rule 20 typed deliverable on test DNS/tunnel (`app-test.example.com`).
* **Canary Promotion & Garbage Collection**:
  * Once the clean-sheet `-test` container passes 100% green, production hardening is verified and promotion is authorized, the git commit/tag is promoted to production via the canary protocol (Rule 25).
  * After retaining necessary evidence and state, the Parent executes scoped destruction of disposable environments (`podman rm -f` / `lxc delete`) of the `-dev` and `-test` containers, releasing all ports, memory, and scratch volumes (Universe Garbage Collector).
* **The maker is the Parent's hand** : in the fractal of Rule 11, the level $K+1$ of an instance is its **governor and the makers that governor enrolled** — the tandem, root from underneath, brought each maker into being and declared it (the maker template's invariant 7). The authority this rule grants — to instantiate, access and destroy a child — is held by the **maker organ of that level**, in its vault, on the one machine it acts on: never by the governor, which writes rows and holds no key to any host, and **it never leaves the level** — no private key crosses down into a child, none climbs up into a ledger. The Parent's public key reaches a child through the stamp recipe, as a file, never as a command built from the row. Birth and end (`lxc launch` / `lxc delete`, `pct create` / `pct destroy`, and for the `nested` shape `podman run` / `podman rm` — or the PodMesh operations that wrap them where PodMesh is installed) are the maker's gestures on a ledger row; the garbage collection above is the same gesture, driven by the row's deadline. The host's own SSH door is the tandem's, from underneath; it is not the maker's, and the maker holds no inbound door of its own.


---

<a id="rule-37"></a>
### Rule 37: The Tree Speaks (Lexicon Closure, Manifest Lineage Fields & the Fleet Map)

* **Three manifest fields carry all lineage — never the slug**:
  * `perimeter`: `P1` | `P2` | `P3`, **mandatory on every declared brick**.
    Perimeter means **LAYER, never OWNER** — a client-specific brick can be P1.
  * `source`: `base` | `catalogue` | `fork` | `native`, mandatory.
    `native` = a P3 brick scaffolded inside the class repo (the
    constructor-generated class realization); `fork` = inherited from a standard brick and
    specialised.
  * `forkedFrom`: `{ "package": "@shaper/pkg-x", "atVersion": "x.y.z" }` —
    **mandatory when `source` is `fork`**, forbidden otherwise. A Rule 33 fork
    repo additionally declares repo-level lineage in its manifest root:
    `"forkedFrom": { "repo": "<upstream>", "atTag": "vX.Y.Z" }` — this is what
    lets `shaper verify` enforce the mirror rule by machine.
* **One state machine, one set of names, everywhere**:
  `DESIRED → RECONCILING → PURRING → DEGRADED`, plus the terminal `REAPED`
  .
  * **PURRING** is the healthy state, and it is **dated**: the universe writes
    it to its `status.json` on every on-time beat when observed == desired.
    Silence is ambiguous between "fine" and "dead and unable to say so"; a
    stale `lastPurr` timestamp is the alarm. `running`, `green`, `OK` and
    every other synonym are forbidden as state words.
  * **drift** is the ONLY word for observed != desired, and the only repair
    trigger. Rule 27 governs the repair ladder and the resting `DEGRADED`.
  * **DEGRADED** rests; it never self-clears. It is left in two ways only
    (Rule 27): by its account's explicit new ask, for the environments a
    robot may end (`dev`, `test`, `demo`) — the broken row's deadline
    becomes now, a maker reaps whatever half-exists, a fresh row is born —
    or, for a `prod` row, by human or Root Guardian action alone.
  * **REAPED** is the end: a maker ended the universe on the row's deadline
    and looked (the reap recipe verifies the absence, it does not assume
    it), or a human ended it. Terminal, and dated by its event. *Prevents*:
    a reaped row still counted as living — its account blocked forever
    behind a slot nothing frees, its matrix pinned by a reference no
    instance holds. A state word for "ended" that did not exist was read
    as "still there".
  * <a id="rule-37-status-json"></a>`status.json` (per instance: state, lastPurr, lastBackup) is the canonical
    surface; every board, cockpit tile or STATE file is a rendering of it,
    never a rival.
* **The ledger is the only instance store**: one row per instance, in the
  governor functional Podman's own private database (Rule 26). The row : `id`, `account`, `klass`, `matrix`,
  `digest`, `machine`, `env`, `state`, `params`, `deadlineAt`, `createdAt`,
  `updatedAt`, `events[]`. What changed from the first reading (class, tag,
  machine, env, state, bucket), and why: `tag` became `matrix` + `digest`,
  because an instance is born from an artefact, not from a repo tag — five
  builds of one commit are five fingerprints, and the digest is what the
  maker proves it holds; `bucket` is derivable (`r2://<id>`) and never
  stored; `id` was missing while the instance's name derives from it;
  `account` is who asked, and with `klass` it is the idempotence key (one
  live row per account and class); `deadlineAt` is the only clock a robot
  reads — a row past it yields reap work, never a timer inside a robot;
  `params` is the typed slot a recipe reads (a flat object of scalars under
  an allow-list the product declares per class; immutable on a living row,
  like its digest; carried to the recipe as `SHAPER_PARAM_<KEY>` on an
  environment the maker builds, never as argv); `events[]` are the dated
  facts makers reported, from which every transition is derived by one
  table. `env` ranks `dev`, `test`, `demo`, `prod`: the first three are
  environments a robot may end; `demo` is what a row carries when it names
  none, and it is not production. **The canonical [governor contract](docs/contracts/governor.md) is binding**, including its state/transition table and work kinds — stamp, reap, validate, adopt. A standalone universe governs itself: its ledger lives in its
  own database inside the governor Podman's boundary. Every functional Podman
  carries its own mandatory MariaDB under Rules 4 and 26; `+data` is therefore
  only a retired compatibility alias and never a shared universe database. The governor persists these records in its own private MariaDB.
  "placement" survives only as the name of the machine-assignment column.
  Tag precedence: **fleet.yml = the default for new instances and the PRA
  floor; the ledger row = the truth, which may lag during a canary; an audit
  task reconciles them.**
<a id="rule-37-fleet-map"></a>
* **The fleet map**: one tiny repo (`<scope>-fleet`) holding one `fleet.yml` —
  base, any catalogue actually used and every class repo pinned to an **immutable tag**
  (Rule 0E), plus the `machines:` inventory. Instances NEVER appear in it;
  R2 buckets are derivable (`r2://<instance-id>`), never enumerated. `-dev`
  bypasses the fleet map by law; `-test` and `-prod` are guarded by it: a
  universe repo not registered in its fleet map is refused promotion. A
  sovereign fork (Rule 33) keeps its own mirrored fleet map — a client's PRA
  never hinges on the vendor's repo.
* **Lexicon closure**: the vocabulary of this architecture is the prefix table
  (Rule 1, canonical in `docs/architecture/NAMING.md`) plus twenty-three words —
  class, instance, ledger, drift, PURRING (and its state machine), status.json,
  board, fleet map, forge, forkedFrom, the mirror rule, source/perimeter, and,
  by the amendment of 2 September 2026 (maker-and-governor verdict, §10),
  governor, maker, matrix, REAPED, and, by the amendment of 4 September 2026,
  rig, tool, and, by the amendment of 16 September 2026 (Rule 11), shape, and,
  by the amendment of 17 September 2026 (one Helm for every pilot, Rule 0F),
  Helm, jurisdiction, root, pilot level.
  A new noun enters only by amending this
  rule, with the failure it prevents written beside it — as here:
  * **governor** — the universe that holds a ledger and makes it respected:
    it writes what should exist, dates what makers report, and never dials
    out. *Prevents*: "the SaaS" and "the manager" naming two things — the
    product and the organ — and the maker learning which one it serves.
  * **maker** — the hand of a machine, one per machine: it asks its governor
    what should exist on its host, runs a frozen recipe with typed
    positions, reports a fact, never decides. *Prevents*: a script on a host
    whose state nobody knows, and a form field reaching a shell.
  * **matrix** — the locked, content-addressed artefact (sha256) from which
    instances are stamped; baked by the tandem from a class, never by a
    robot. *Prevents*: "image" meaning both a podman image and a universe
    archive, and five builds of one commit giving five fingerprints.
  * **REAPED** — the fifth, terminal state, above. *Prevents*: a reaped row
    still counted as living, blocking its account and pinning its matrix.
  * **rig** — the assembled solution: the classes it takes, the bricks they
    declare, and the declarations that shape them (sector profile, tool
    catalogue, seed), pinned together. A rig is NOT a class: a class is one
    repo, a rig is what is delivered — the demo rig is `univ-demo-saas` and
    `univ-demo-crm` and the entry door and the maker, at named tags.
    *Prevents*: "the demo" meaning one repo to the person building it, two
    repos to the person deploying it, and the whole visitor chain to the
    person selling it — so that what a client buys has no name, no version,
    and no way to be assembled twice the same.
  * **tool** — one declared capability a class exposes to its agent, with a
    typed contract, from a closed catalogue: the agent may fill it and execute within the human-approved action or action-type policy; approval already embodied in that policy is not requested again. *Prevents*: `tool` naming
    both a deliverable unit and an agent's capability (the unit is a brick);
    and free text reaching an action because the catalogue of what may be
    asked was never declared anywhere.
  * **shape** — what a universe's container is, declared by its class
    (`shape` in `manifest.json`, `lxc` when absent): `lxc` or `nested`
    (Rule 11). A host family is how a machine makes that container; a machine
    may offer several. *Prevents*: one token naming both what a universe is
    and how a host builds it, so that a machine offering LXD and rootful
    Podman cannot be described, and a class cannot say which container it
    needs.
  * **Helm** — the conversational interface between a human and the
    ecosystem in their charge, web or mobile web, text or voice, set by a
    jurisdiction and a pilot level and by nothing else; it sends requests to
    Runtime and never holds authority (Rule 0F). `brick-helm` implements it
    and its local owning intent specifies it: the word names that contract across
    classes, not one brick, which is why it enters where `steward` did not.
    *Prevents*: KovZu, Helm and "Control Hub" naming one surface under three
    authority models, so that an operator's cockpit and a client's portal
    were designed twice and a customer's question had no defined boundary.
  * **jurisdiction** — the universes a pilot is in charge of, down to their
    constituent pods, granted by the root above; Helm sees nothing and answers
    for nothing outside it. Jurisdictions nest: a root may grant a narrower
    jurisdiction inside its own, never a wider one. *Prevents*: "tenant",
    "galaxy", "portfolio" and "scope" naming four perimeters for one question —
    what may this person see and change? — and a client's agent answering
    with another client's universe.
  * **root** — full power over a jurisdiction, held by a human–agent tandem,
    reaching underneath its universes to their pods. Two strata, never more.
    The **master root** is the founding tandem at the top of the fractal: root
    from underneath every host (Rule 36), sole director of the governor and
    the makers, keeper of matrices and backup contracts, grantor of every
    jurisdiction, and the holder of Rule 24's root universe. A **jurisdiction
    root** is the tandem a jurisdiction is granted to (a client and its agent
    at the Helm of their Workspace or Vox): full power inside it; none over a
    host, the governor, a maker, a matrix, a class repo, another jurisdiction
    or its own backup contract. *Prevents*: "root" meaning only the top of the
    tree, so that a client entrusted with their own universe was either denied
    the power they are given or silently handed the host beneath it.
  * **pilot level** — what a person at the Helm has validated for one class,
    from E0 to E5: familiar work, ask Helm, delegate once, pilot, standing
    mandate, shape the environment. It is proven by pilot training in a `demo`
    instance of that class, never declared, and a level proven on one class
    says nothing about another. Root and mandate say what a pilot may do; the level says what
    Helm executes directly for that person, and above it Helm prepares the
    change and routes it for validation instead of acting. *Prevents*:
    authority read as competence — a jurisdiction root applying to production
    a change they could not yet name, because owning a universe was taken for
    knowing how to steer it.
  What the amendment of 17 September 2026 keeps out: `KovZu` and
  `Control Hub` (a retired and a refused synonym of Helm); `pilot training`
  and `blank universe` (an activity inside a `demo` instance and a TARGET
  offer, described where they live, not nouns of the tree); `Steward`, which
  names the human of a root tandem in the architecture documents and remains
  `brick-steward` here.
  What does not enter: `stamp`, `reap`, `validate`, `adopt` — kinds of work,
  a table in `pkg-governor`, not nouns of the language. New bricks are not
  new nouns — `brick-forge`, `brick-scraper`, `brick-sso` are the prefix
  system doing its job. The forge's line is bounded by the same amendment:
  `brick-forge` deploys, destroys and repairs BRICKS inside a living universe
  (the brick level; drift at brick level); universes are born and ended by
  the maker, from a ledger row (the universe level; the gap at instance level).
* **What it protects**: a human juggling several vibecoded projects and a cold
  agent landing in a repo must both answer, from one page — *where is the
  truth?* (the ledger) — *who repairs?* (the forge, on drift, inside a
  universe) — *who births?* (the maker, from a row) — *is everything fine?*
  (the board, rendering status.json) — *how is it all recreated?* (the fleet
  map + R2, Rule 16) — *who may act here?* (the root of this jurisdiction,
  through Helm, at its pilot level). A vocabulary that cannot fit on one page has already
  failed them both. `docs/architecture/LEXICON.md` is that page, and the realization verifies that its manifests, interfaces and state machine use that same vocabulary.
