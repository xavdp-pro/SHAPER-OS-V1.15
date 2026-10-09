# Rules 32–36 — Generic construction, fractal forks and bridges

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
The original rule identifiers, scope and binding force are unchanged.

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


Security boundaries are designed during DEV and necessary functional protections are implemented then. Detailed production hardening follows integrated acceptance, as specified in [Lifecycle](../../docs/agent/LIFECYCLE.md); it is not waived by generic-first construction.

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


## Reading continuation

[Previous part](05-REPAIR-AND-DATA.md) · [Next part](07-TREE-AND-FLEET.md)
