# SHAPER OS & UNIV — Fundamental Engineering Rules & Architecture Invariants

<a id="canon-preamble"></a>
This index and the seven linked rule files form the **canon**. Read the index
and every rule file in full; neither a summary nor the index alone replaces that reading. Rules are added, never removed to fit what the code currently does —
when intent and implementation diverge, record the gap in the realization and correct it; a gap does not waive the contract.

---

## How to read this file

The orientation and work-routing tables below are reading aids, not inventories
of all 49 rules. They never replace the [complete rulebook](#complete-rulebook).

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

## Current construction scope

This is the complete local V1.15 rulebook. [The self-contained adoption decision](decisions/2026-10-06-SELF-CONTAINED-CORPUS.md) and the [6 October construction and execution direction](decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md) govern the present scope. Implementation artifacts named below are produced in the separate realization, not supplied by this code-free OS. The constructor generates missing code and precise contracts; only a genuinely undecided authority/business policy blocks its dependent action. A protection boundary is not a CLI permission prompt: authorized DEV executes fully, and production applies the tandem's verified per-action/type rights.

## Why the rulebook is split

**[EDITORIAL] Reading structure:** some agent tools cap an individual file read
by bytes or tokens. A large file can be truncated even when the agent requests
every line; a plausible summary does not prove that the omitted rules were read.
The rulebook is divided into smaller files to make complete reading easier to
deliver, resume and verify. This changes storage and navigation, not the rules,
their identifiers, applicability or binding force. There is one canonical body
for each rule, not separately maintained copies.

All seven parts remain mandatory. Smaller files do not guarantee understanding
or permanent context retention. Detect truncated output, resume from the next
actually delivered section, keep revision and coverage evidence, and reload the
exact affected rules before action as described in the
[reading contract](docs/READING-CONTRACT.md#complete-reading-through-bounded-outputs).

<a id="complete-rulebook"></a>
## Complete rulebook

Read the preamble above, then every part below in order, then the applicable
contracts identified by the [governing corpus](docs/GOVERNING-CORPUS.md).
The seven files own the full rule text. The legacy locators below only preserve
navigation for existing links; they do not contain a shortened rulebook.

| Part | Rules | Canonical owner |
| :--- | :--- | :--- |
| 1 | 0–0K | [Foundation and collaboration](docs/rules/01-FOUNDATION.md) |
| 2 | 1–5 | [Naming, construction and native tests](docs/rules/02-CONSTRUCTION.md) |
| 3 | 6–12 | [Agents, execution, containment and recovery](docs/rules/03-EXECUTION-AND-CONTAINMENT.md) |
| 4 | 13–22 | [Services, interfaces and typed quality](docs/rules/04-SERVICES-AND-QUALITY.md) |
| 5 | 23–31 | [Repair authority and data integrity](docs/rules/05-REPAIR-AND-DATA.md) |
| 6 | 32–36 | [Generic construction, fractal forks and bridges](docs/rules/06-FRACTAL-CONSTRUCTION.md) |
| 7 | 37 | [Tree vocabulary, lineage and fleet](docs/rules/07-TREE-AND-FLEET.md) |

## Stable rule locators

Follow each locator to its complete canonical body. Subrule locators retain
their original target text in that same owner.

<a id="rule-0-language-collaboration-protocol"></a>
<a id="rule-0"></a>
### Rule 0: Language & Collaboration Protocol (Total Invariant)

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0).

<a id="rule-0a"></a>
### Rule 0A: Three Perimeters Taxonomy (P1 / P2 / P3)

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0a).

<a id="rule-0b"></a>
### Rule 0B: Universal Parametric Genericity Invariant (Zero Hardcoding)

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0b).

<a id="rule-0b-intent-header-classification"></a>
[Complete provision: `rule-0b-intent-header-classification`](docs/rules/01-FOUNDATION.md#rule-0b-intent-header-classification).

<a id="rule-0c"></a>
### Rule 0C: Declarative Agent-First Simplicity

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0c).

<a id="rule-0d"></a>
### Rule 0D: Dual Intent & Topology Manifest Protocol (INTENT.md + JSON)

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0d).

<a id="rule-0e"></a>
### Rule 0E: Materialization Pipeline (Intent → Construction → Proof → Reuse)

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0e).

<a id="rule-0f"></a>
### Rule 0F: Helm Is the One Human Interface to an Ecosystem; Business Tools Stay Distinct Applications

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0f).

<a id="rule-0g"></a>
### Rule 0G: Strict "NO FAKE, NO FALLBACK" Testing & Validation Invariant

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0g).

<a id="rule-0h"></a>
### Rule 0H: Universal Interchangeable CLI Matrix & Human-Arbitrated Economics

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0h).

<a id="rule-0i"></a>
### Rule 0I: Pure IA-Driven Installation Doctrine (Zero Installer Monoliths / Pure Intent Synthesis)

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0i).

<a id="rule-0j"></a>
### Rule 0J: Human–Agent Construction and Required Secrets

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0j).

<a id="rule-0j-zero-blind-execution"></a>
[Complete provision: `rule-0j-zero-blind-execution`](docs/rules/01-FOUNDATION.md#rule-0j-zero-blind-execution).

<a id="rule-0k"></a>
### Rule 0K: Channel Authentication, Explicit Outcomes and Session Rebirth

Read [the complete rule](docs/rules/01-FOUNDATION.md#rule-0k).

<a id="rule-1"></a>
### Rule 1: Canonical Naming Conventions & the Universe Repo Grammar

Read [the complete rule](docs/rules/02-CONSTRUCTION.md#rule-1).

<a id="rule-2"></a>
### Rule 2: Atomic Git Changes with Declared Authorship

Read [the complete rule](docs/rules/02-CONSTRUCTION.md#rule-2).

<a id="rule-3"></a>
### Rule 3: Podman Images and Service Management

Read [the complete rule](docs/rules/02-CONSTRUCTION.md#rule-3).

<a id="rule-4"></a>
### Rule 4: Standard Application Layout & Per-Functional-Podman Database Isolation

Read [the complete rule](docs/rules/02-CONSTRUCTION.md#rule-4).

<a id="rule-5"></a>
### Rule 5: Native Unit and Contract Tests

Read [the complete rule](docs/rules/02-CONSTRUCTION.md#rule-5).

<a id="rule-6"></a>
### Rule 6: Targeted Agent Bootstrapping (Token Optimization & Zero Idle Waste)

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-6).

<a id="rule-6-decision-hygiene"></a>
[Complete provision: `rule-6-decision-hygiene`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-6-decision-hygiene).

<a id="rule-7"></a>
### Rule 7: Engine Defaults Are Measured, Never Declared

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-7).

<a id="rule-8"></a>
### Rule 8: Universal Agent HTTP Contract

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-8).

<a id="rule-9"></a>
### Rule 9: Strict Mailbox Isolation (Test/Dev vs Prod)

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-9).

<a id="rule-10"></a>
### Rule 10: DEV, TEST, PROD and Three Recovery Clocks

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-10).

<a id="rule-10-destroy-after-test"></a>
[Complete provision: `rule-10-destroy-after-test`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-10-destroy-after-test).

<a id="rule-10-zero-duration-figure"></a>
[Complete provision: `rule-10-zero-duration-figure`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-10-zero-duration-figure).

<a id="rule-11"></a>
### Rule 11: Two Levels of Containment and Recovery Integrity

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11).

<a id="rule-11-nftables-inside-the-universe"></a>
[Complete provision: `rule-11-nftables-inside-the-universe`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-nftables-inside-the-universe).

<a id="rule-11-read-profiles-with-config-show"></a>
[Complete provision: `rule-11-read-profiles-with-config-show`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-read-profiles-with-config-show).

<a id="rule-11-nesting-needs-a-restart"></a>
[Complete provision: `rule-11-nesting-needs-a-restart`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-nesting-needs-a-restart).

<a id="rule-11-declared-ports-are-free"></a>
[Complete provision: `rule-11-declared-ports-are-free`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-declared-ports-are-free).

<a id="rule-11-what-is-restored"></a>
[Complete provision: `rule-11-what-is-restored`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-what-is-restored).

<a id="rule-11-a-brick-is-rebuilt-not-repaired"></a>
[Complete provision: `rule-11-a-brick-is-rebuilt-not-repaired`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-a-brick-is-rebuilt-not-repaired).

<a id="rule-11-a-brick-runs-as-its-own-class-not-root"></a>
[Complete provision: `rule-11-a-brick-runs-as-its-own-class-not-root`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-11-a-brick-runs-as-its-own-class-not-root).

<a id="rule-12"></a>
### Rule 12: Secure Archive Distribution & Cold Recovery

Read [the complete rule](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12).

<a id="rule-12-what-a-backup-archive-never-contains"></a>
[Complete provision: `rule-12-what-a-backup-archive-never-contains`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-what-a-backup-archive-never-contains).

<a id="rule-12-key-does-not-travel-with-the-coffer"></a>
[Complete provision: `rule-12-key-does-not-travel-with-the-coffer`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-key-does-not-travel-with-the-coffer).

<a id="rule-12-backup-key-is-its-own"></a>
[Complete provision: `rule-12-backup-key-is-its-own`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-backup-key-is-its-own).

<a id="rule-12-dump-not-taken-is-announced"></a>
[Complete provision: `rule-12-dump-not-taken-is-announced`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-dump-not-taken-is-announced).

<a id="rule-12-archive-failure-is-backup-failure"></a>
[Complete provision: `rule-12-archive-failure-is-backup-failure`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-archive-failure-is-backup-failure).

<a id="rule-12-complete-archive-is-kept"></a>
[Complete provision: `rule-12-complete-archive-is-kept`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-complete-archive-is-kept).

<a id="rule-12-failed-dump-leaves-nothing"></a>
[Complete provision: `rule-12-failed-dump-leaves-nothing`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-failed-dump-leaves-nothing).

<a id="rule-12-env-in-every-spelling"></a>
[Complete provision: `rule-12-env-in-every-spelling`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-env-in-every-spelling).

<a id="rule-12-client-call-proven-with-a-recorder"></a>
[Complete provision: `rule-12-client-call-proven-with-a-recorder`](docs/rules/03-EXECUTION-AND-CONTAINMENT.md#rule-12-client-call-proven-with-a-recorder).

<a id="rule-13"></a>
### Rule 13: Hybrid WireGuard Private Mesh Network & Mandatory Peer Naming

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-13).

<a id="rule-13-peer-comments"></a>
[Complete provision: `rule-13-peer-comments`](docs/rules/04-SERVICES-AND-QUALITY.md#rule-13-peer-comments).

<a id="rule-14"></a>
### Rule 14: Efficient Visual and Programmatic Control

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-14).

<a id="rule-15"></a>
### Rule 15: Media Art Direction & Industrial Realism

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-15).

<a id="rule-16"></a>
### Rule 16: Multi-level backup (container → files tar.bz2 → database → git → S3)

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-16).

<a id="rule-16-archive-hygiene-scope"></a>
[Complete provision: `rule-16-archive-hygiene-scope`](docs/rules/04-SERVICES-AND-QUALITY.md#rule-16-archive-hygiene-scope).

<a id="rule-17"></a>
### Rule 17: Mandatory TTS Phonetic Dictionary, Acronym Expansion & Fine Word Karaoke

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-17).

<a id="rule-18"></a>
### Rule 18: Primary Admin Account Onboarding Protocol (Zero Unsolicited Dummy Users)

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-18).

<a id="rule-19"></a>
### Rule 19: Dual Semantic Register & The Toggle Law (Zero Jargon in Simple Mode)

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-19).

<a id="rule-20"></a>
### Rule 20: Typed Closed-Loop Quality Gate (Verification Before Delivery)

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-20).

<a id="rule-20-functional-test-means"></a>
[Complete provision: `rule-20-functional-test-means`](docs/rules/04-SERVICES-AND-QUALITY.md#rule-20-functional-test-means).

<a id="rule-20-record-what-actually-happened"></a>
[Complete provision: `rule-20-record-what-actually-happened`](docs/rules/04-SERVICES-AND-QUALITY.md#rule-20-record-what-actually-happened).

<a id="rule-21"></a>
### Rule 21: Distributed Multi-Agent Delegation Matrix (Abstract Capacity Classes)

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-21).

<a id="rule-22"></a>
### Rule 22: Automatic Semantic Memory Ingestion & Multi-Tenant Vector Isolation (RAG)

Read [the complete rule](docs/rules/04-SERVICES-AND-QUALITY.md#rule-22).

<a id="rule-22-isolated-qdrant-collection"></a>
[Complete provision: `rule-22-isolated-qdrant-collection`](docs/rules/04-SERVICES-AND-QUALITY.md#rule-22-isolated-qdrant-collection).

<a id="rule-23"></a>
### Rule 23: External Healing Law (Parent Repairs Child)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-23).

<a id="rule-24"></a>
### Rule 24: Root Guardian Law (Sentinel / Human Repairs Root)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-24).

<a id="rule-25"></a>
### Rule 25: Canary Deployment & Downward Rollback (Anti-Propagation)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-25).

<a id="rule-26"></a>
### Rule 26: Complete Database Isolation (MariaDB per Functional Podman)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-26).

<a id="rule-27"></a>
### Rule 27: Reconciliation Convergence Guard (Anti-Flapping & Resting Degraded State)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-27).

<a id="rule-28"></a>
### Rule 28: Sovereign WAF Rule Validation (No Unproven Guardian)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-28).

<a id="rule-29"></a>
### Rule 29: Constructive Integrity (Every Fixed Bug Becomes a Test)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-29).

<a id="rule-30"></a>
### Rule 30: Snapshot Before Migration (Data-Bearing Changes Are Not Canary-able)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-30).

<a id="rule-31"></a>
### Rule 31: Declared Data Lifecycle (Per Universe, Not a Universal Policy)

Read [the complete rule](docs/rules/05-REPAIR-AND-DATA.md#rule-31).

<a id="rule-32"></a>
### Rule 32: The Perfected Generic Base Comes Before Any Specialisation (Founding Method)

Read [the complete rule](docs/rules/06-FRACTAL-CONSTRUCTION.md#rule-32).

<a id="rule-33"></a>
### Rule 33: The Client Fractal Fork (Assumed Divergence, Never Contamination)

Read [the complete rule](docs/rules/06-FRACTAL-CONSTRUCTION.md#rule-33).

<a id="rule-34"></a>
### Rule 34: A Bridge Ships Everything Its CLI Needs (Prerequisites Are Declared, Pinned and Proven)

Read [the complete rule](docs/rules/06-FRACTAL-CONSTRUCTION.md#rule-34).

<a id="rule-35"></a>
### Rule 35: Experience Corrects the Intent, Not Only the Code (Constructive Integrity, Upstream)

Read [the complete rule](docs/rules/06-FRACTAL-CONSTRUCTION.md#rule-35).

<a id="rule-36"></a>
### Rule 36: Fractal SSH Authority & Ephemeral Sandbox Access Law (Clean-Sheet Dev/Test Promotion)

Read [the complete rule](docs/rules/06-FRACTAL-CONSTRUCTION.md#rule-36).

<a id="rule-37"></a>
### Rule 37: The Tree Speaks (Lexicon Closure, Manifest Lineage Fields & the Fleet Map)

Read [the complete rule](docs/rules/07-TREE-AND-FLEET.md#rule-37).

<a id="rule-37-status-json"></a>
[Complete provision: `rule-37-status-json`](docs/rules/07-TREE-AND-FLEET.md#rule-37-status-json).

<a id="rule-37-fleet-map"></a>
[Complete provision: `rule-37-fleet-map`](docs/rules/07-TREE-AND-FLEET.md#rule-37-fleet-map).
