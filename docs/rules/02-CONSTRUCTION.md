# Rules 1–5 — Naming, construction and native tests

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
Original rule identifiers remain stable. Current scope follows the explicit
[25 October direction](../../decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md); earlier adopted revisions retain their recorded boundaries.

<a id="rule-1"></a>
### Rule 1: Canonical Naming Conventions & the Universe Repo Grammar

* **The compatible `univ-*` class-repository grammar** (for repositories using this lineage): `univ-<project>-<class>`, where
  **project is ONE word, no hyphen** — everything after the first word is the
  class, which may be composite. One-line parse:
  `^univ-[a-z0-9]+(-[a-z0-9]+)+$`. A single-class project takes `-core`
  (`univ-mailo-core`): five characters against a future rename, settled.
  The grammar follows the programming metaphor of a class and its
  instantiation: the repository defines the class; each instance materializes
  it with its own identity, environment and state. In this lineage “universe”
  keeps its earlier sense of one operational composition, usually a specialized
  cell; see the [27 October vocabulary direction](../../decisions/2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md).
* **Source roles are explicit.** Mental frameworks, glossary, ecosystem map,
  domain intentions, implementation products and fleet definitions retain their
  owning sources. Every project has a distinct product repository and private
  `-lab` companion for work/discussions/evidence. Public mental sources and private
  SaaS/VOX implementations remain separate. The [source-role index](../architecture/SOURCE-ROLES.md)
  defines custody; the old base/catalogue/universe/fork/fleet names remain
  compatibility conventions, not an exhaustive list of repositories.

* **A release is an independently readable slice**: its full governing documentation lives in its own repository; implementation releases live in their separate realization repositories. Fleet records pin repository and immutable tag. Independent releases may run side by side; changes are deliberately carried and qualified, never presumed inherited. Verify the destination remote before the first authorized push of a copied workspace.

* **The mirror rule (Rule 33 forks)**: a fork swaps **only the project word**
  and keeps every class word, repo kind and file name verbatim
  (`univ-boutik-shop → univ-fortex-shop`). A fork costs zero new vocabulary,
  and `shaper verify` can hold it via the repo-level `forkedFrom`.
* **Classes are versioned definitions; instances have stable identities.** A
  specialization records its inherited base and domain delta. Its source repository
  owns the reusable definition; an instance is represented by its ledger and owned
  durable state. Private realization/configuration repositories may describe an
  instance without becoming its identity or a rival runtime ledger. Runtime instance names follow the triumvirate lifecycle
  (`<slug>-dev`, `<slug>-test`, `<slug>-prod`, Rule 36); DNS names are declared by the realization and remain unique within its domain.
* **Package and functional-unit prefixes are unchanged**:

| Element Type | Scope / Layer | Canonical Naming Convention | Real-World Examples |
| :--- | :--- | :--- | :--- |
| Composable logic packages | NPM Scope `@shaper/` | `@shaper/<brick>` | `@shaper/pkg-vault`, `@shaper/pkg-logger`, `@shaper/pkg-queue` (**P1**); `@shaper/pkg-maestro`, `@shaper/pkg-mail-agent`, bridges (**P2**) |
| Deployable functional units | OCI images | `brick-<name>` / `img-<name>` | `brick-vault`, `brick-forge`, `img-logger` |

* **Component Isolation Invariant**: A `@shaper/*` package never has knowledge of the cell or universe consuming it (zero coupling, 100% isolated unit test coverage).
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
* **Standard Application File Structure (`/apps/<slug>/`)**: Every deployed application or service component adheres strictly to the canonical application filesystem hierarchy — **same spirit under Podman**: persist what must survive in bind-mounted volumes, never mix cache with backups:
  ```
  /apps/<slug>/          # or <univ>/ for a Podman universe
  ├── app/               # Code (git) — not a substitute for volume backup
  ├── etc/mysql/localhost/passwd
  ├── log/               # Diagnostic streams/exports; authoritative logs in MariaDB
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
  * **The Turbinobash Method: One Application Account per Server**: the clauses
    above form one method, the one to apply whenever an application is built. It
    comes from Turbinobash (`tb`, [turbinobash-web](https://github.com/xavdp-pro/turbinobash-web)):
    on a Turbinobash host each application is one Linux account, one MariaDB
    account and one database carrying the application's name, with its password
    in its own `etc/mysql/localhost/passwd`. Under SEP22-CONTAINER-MARIADB a
    functional unit is one such application, with a MariaDB server of its own
    that serves it alone. SHAPER inherits the method, not Turbinobash's scripts:
    their grants, password handling and ownership changes are not a qualified
    realization of this profile. The points below present the clauses above in
    the order a unit is built, and add what those clauses leave implicit.
    1. **One application account.** One declared functional identity names the
       application's Linux account, its MariaDB account and its database. Its
       home is `/apps/<functional-slug>/` as seen inside the container. That
       directory and the database, socket and administrative paths beneath it
       are owned by root or by the engine account, never by the application
       account: an owner could rename `sav/` aside and plant its own data
       directory. The application account owns only what it writes — its
       password file and its declared application data paths. An upstream
       application account may be that identity when it is declared
       consistently everywhere; the database engine's `mysql` account and root
       stay distinct and keep their qualified internal identities (Rule 11). The
       application never runs as root, and no ownership change over the MariaDB
       data or administrative files is ever recursive.
       Choosing an upstream account name does not waive Rule 11's fixed numeric
       UID above 1000 for own application code; documented upstream service
       identities keep their separately applicable Rule 11 treatment.
       Qualification records the actual process identities and the ownership of
       the persistent volumes.
    2. **One MariaDB server in the same container.** The application and its
       private MariaDB server run as separate processes in the same functional
       application container. The server runs under its distinct, qualified,
       non-root engine account (`mysql`). It listens only on a private local Unix
       socket, never on TCP, and that socket is not exposed to other functional
       units. A separate database container does not satisfy this requirement,
       including one in the same Podman pod. The data directory, socket
       directory and administrative configuration are protected against
       modification or replacement by the application account, including
       through writable ancestor directories; the application receives only the
       filesystem access required to connect to the private socket.
    3. **The same name for the account and the database.** The application
       account receives only the runtime data privileges its contract declares,
       confined to its application database: no administrative privilege, no
       grant option and no schema-management privilege. Schema initialization
       and migrations use the separate authorized local administrative path,
       with Rule 30 protection before data-bearing changes.
    4. **One password file.** The password is generated on first initialization
       into `/apps/<functional-slug>/etc/mysql/localhost/passwd` (mode `0600`,
       owned by the application account) and never passed on a command line.
       The application reads it there and takes its database user and database
       name from its declared identity. Recreation preserves and validates the
       existing database and credential continuity; rotation follows an
       explicit, recovery-safe procedure.
    5. **Root administers through its own path**: the local root command line
       through its declared authentication mechanism, Unix-socket
       authentication included. The application receives neither administrative
       credentials nor administrative privileges.
    6. **Recovery point.** Each unit's recovery point includes a consistent
       logical dump of its application database, coordinated with its declared
       non-reproducible volumes and versioned reconstruction records. Rules 12,
       16 and 30 govern protection, completeness and restore proof.
* **Complete Application State**: authoritative business records, logs, scheduler
  registrations and occurrences, leases, pending work, action records, durable
  CLI sessions, context revisions and engine-session mappings belong in the
  private MariaDB of their functional owner. Native tool files and exported
  JSONL are working material or projections, with explicit reconstruction.
  Durable media/artifacts have database-owned references and declared storage.
* **Partitions by Workload**: choose physical SQL table partitioning where data
  volume, queries, maintenance and retention justify it; ordinary tables remain
  valid. A selected UTC-month history policy declares keys, boundaries, indexes,
  forward partitions and bounded catch-alls. Administrative DDL stays separate
  from the application account. Retention authorizes deletion independently of
  partition rollover. Consistent dump/restore preserves selected definitions and
  retained rows. The [25 October direction](../../decisions/2026-10-25-COMPOSITION-OWNERSHIP-AND-CONTINUITY.md)
  narrows the earlier general monthly requirement.

* **Continuous Architectural Traceability**: Document every architectural choice with *What* (concise description) and *Why* (business rationale).

---

<a id="rule-5"></a>
### Rule 5: Native Unit and Contract Tests
* A 100% pass rate for the complete applicable native/unit and contract suite is required before staging or production promotion. Generate meaningful tests for the selected implementation.
* Use the selected language's native test facilities and avoid unnecessary heavyweight frameworks. In a Node.js realization, the native runner is `node --test` and the cold test-process startup budget is 2000 ms; measure that scoped test budget rather than presenting it as a universe boot or recovery promise.
* The OS does not require every implementation to use Node.js. Language choice remains subject to the agnostic construction direction and the owning unit's actual contract.

---


## Reading continuation

[Previous part](01-FOUNDATION.md) · [Next part](03-EXECUTION-AND-CONTAINMENT.md)
