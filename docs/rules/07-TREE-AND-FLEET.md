# Rules 37 — Tree vocabulary, lineage and fleet

This file is a canonical part of the [complete rulebook](../../RULES.md#complete-rulebook).
Read all seven parts in order. The index is navigation, not a substitute for the rule bodies.
The original rule identifiers, scope and binding force are unchanged.

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
  none, and it is not production. **The canonical [governor contract](../../docs/contracts/governor.md) is binding**, including its state/transition table and work kinds — stamp, reap, validate, adopt. A standalone universe governs itself: its ledger lives in its
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

## Reading continuation

[Previous part](06-FRACTAL-CONSTRUCTION.md) · [Reading contract](../READING-CONTRACT.md#complete-reading-through-bounded-outputs)
