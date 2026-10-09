# Rules 0–0K — Foundation and collaboration

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
The original rule identifiers, scope and binding force are unchanged.

<a id="rule-0"></a>
### Rule 0: Language & Collaboration Protocol (Total Invariant)
* **English for All Technical Assets**: 100% of source code, variable/function names, API schemas, JSON payloads, Git commit messages, branch names, technical specifications, and repository documentation (`README.md`, `RULES.md`, `ctx-universe.md`) MUST be written strictly in **English**.
* **French for Human-Agent Pair Programming**: All strategic discussions, planning sessions, architectural reflections, live brainstormings, and human interactions are conducted fluently in **French**.
* **Zero Mixing Enforcement**: Never write French comments, docstrings, or technical documentation in code repositories. Never respond to the human operator in English unless quoting an exact external error or artifact.

---

<a id="rule-0a"></a>
### Rule 0A: Three Perimeters Taxonomy (P1 / P2 / P3)

Every component, package, brick, or app MUST be classified into **exactly one** perimeter before design or deploy. Canonical source: [perimeter taxonomy](../../docs/architecture/PERIMETERS.md).

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
* **Validation**: Any `doctor`, bootstrap, or deploy script MUST read `topology.json` for ordering — never hardcode dependency chains in shell scripts. The constructor supplies graph validation against `topology.json` and actual imports, following the [topology contract](../../docs/architecture/TOPOLOGY.md).

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
    selection is [`docs/architecture/COGNITION.md`](../../docs/architecture/COGNITION.md): work declares the reasoning
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

The common [cognition-bridge intent](../../docs/intents/cognition-bridge.md) owns session, context, ledger and execution semantics. OpenCode is the selected reference composition, not universal provider law.

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
  * If an environment configuration or port needs adjustment, the AI agent adapts dynamically within the declared parameters and mandate. Apply [Rule 11's port-conflict contract](../../RULES.md#rule-11-declared-ports-are-free): identify the holder and record the resolution; do not silently substitute a declared port or stop an unrelated service. Ordinary choices already covered by the mandate require no repeated approval.
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
* Use the declared DEV execution mode and production action policy in the [common bridge contract](../../docs/intents/cognition-bridge.md). Security design begins with construction; dedicated hardening follows integrated functional acceptance.

---

<a id="rule-0k"></a>
### Rule 0K: Channel Authentication, Explicit Outcomes and Session Rebirth

* A configured channel credential replaces stale consumer configuration. Its caller and receiver must agree on authentication for `/reset`, `/clear`, `/stop` and `/inject`; tokens may be scoped per channel. Do not require one shared all-powerful token across Helm, Bridge, Queue and Maestro.
* A terminal or idle bridge event must yield a visible final outcome. Surface tool aborts, timeouts and errors explicitly. If there is no text result, produce an honest status summary, never fabricated completion; the interface and voice surface must not hang silently.
* Reborn clears the requested conversation and local timeline, immediately loads the current authorized Presentation Briefing and context, and retains the returned Prime run in the UI. It does not erase business records, completed-action evidence or unresolved effects. Reconcile those before further action.
* Changes to a pipeline require its own closed-loop test: unit tests prove parts, the loop proves their interaction. That test belongs to the owning realization; generate it when absent. A simulated loop cannot qualify real bridge, voice or business execution.
* Conversation history, current context and the owning unit's durable action ledger have distinct roles; apply the [common continuity contract](../../docs/intents/cognition-bridge.md).

---


## Reading continuation

[Rule index](../../RULES.md) · [Next part](02-CONSTRUCTION.md)
