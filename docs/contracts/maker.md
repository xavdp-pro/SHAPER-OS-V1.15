# Maker Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

## 1. Declarative Objective

The hand of a machine. It asks its **governor** what should exist on
its host, stamps universes from matrices, reports what happened, and goes
back to asking. A governor is whatever universe holds the ledger it serves —
a demo SaaS today, a fractal manager tomorrow: the maker learns nothing about
which, it reads where to ask. For automated fleet lifecycle work, it is the actor that can create a child universe that does not yet exist; it operates at the parent/host level, never inside the child it must create, and holds the authorized host capability. A human–constructor tandem may bootstrap an isolated first universe directly on its authorized host before a governor or maker exists. The tandem creates these organs when the intended automation needs them; they are not prerequisites for first construction. It is a robot: it does not decide, it does not interpret,
it does not improvise.

## 2. Invariants

1. <a id="never-command-a-host"></a>**Nothing can open a connection to
   it.** It listens on nothing and holds no certificate. It calls outward to
   ask for work and to report; a stolen credential lets someone impersonate
   a worker, never command a host — and, since the governor binds every
   report to the machine the row names, it may lie about its own host's
   rows, never about another's. *(Doctrine: the direction of the link is
   the boundary.)*
2. <a id="typed-parameters"></a>**It executes a frozen recipe with typed
   parameters.** Data that came from a form never becomes part of a
   command: arguments are passed, never concatenated into a shell string.
   Pulling work is not permission to interpret it. Two channels, and only
   two: the six positions of argv (rowId, class, matrix, digest, account,
   env), and the row's `params` as `SHAPER_PARAM_<KEY>` variables on an
   environment the maker BUILDS for the run — the host's few words a CLI
   needs (PATH, HOME, locale), the operator's own `SHAPER_*`
   configuration, and the row's allow-listed keys, held here to the same
   grammar the governor enforces (`^[a-z][a-z0-9_]{0,31}$`, scalars only)
   because a maker holding root trusts no ledger it cannot read. Never
   `process.env` handed down: an inherited environment is how a row
   carrying `LD_PRELOAD` or `BASH_ENV` would have reached a shell running
   as root. A work item carrying a key the grammar refuses is not run and
   not quietly cleaned — the run is refused and the refusal, naming the
   keys, rides the failure event into the ledger.
3. **It never chooses.** Which machine, which matrix, birth or move: the
   governing SaaS decides and writes it in the ledger. The maker only
   reconciles what it reads with what it observes.
4. **Its lanes are the capacity of its host, set from above.** It never
   widens itself: a child asking whether it deserves more is judge and party.
   *(Rule 23.)*
5. **It declares itself by its hostname, never by a configured name.** Its
   identity is the host it can actually act on, asked of that host, not a
   label written in a file that can drift from reality. The same discipline
   as a digest: the thing itself, never the name given to it.
6. **It declares what it holds.** At every poll it states its host, its
   version, its lanes and the matrices it actually carries with their
   digests. A universe is never assigned to a machine that has not proven it
   holds the bytes.
7. **It is created and enrolled by the tandem, and never enrols itself.** A
   human and their agent — root on the system, coming in from underneath —
   bring a maker into being and declare it to its governor. Self-enrolment
   would mean that whoever can run a maker can join the fleet; the fleet is
   not a place one walks into.
8. **Its silence is an event.** The poll is the heartbeat: nothing to do is a
   maker that calls and leaves empty-handed; a dead maker is a host that
   stopped calling. Absence beyond the declared interval is a drift and
   leaves out of band (Rule 27), never a green tile.
9. **Two credentials, never confused.** The one that speaks to the governor may
   only ask and report. The one that acts on the host is the machine's own
   power, held in the maker’s own protected secret store, reachable by no one.
10. **A birth is reported from facts, never from an exit code.** A stamp
   recipe ends with one line of facts — what the host observed of the child
   — and a stamp whose output holds none is reported as a failure, not a
   birth: an end is proven by the recipe's exit code (absence verified, or
   not), a birth only by the facts it looked at.
11. **A refusal is reported under its own name.** A recipe may refuse — an
   unverified matrix, an absent one, a production universe asked to end —
   and says so by its exit code. The reap’s refusal has a name of
   its own (exit 4 → `REAP_REFUSED`), because it is the one the governor
   would otherwise offer again at every beat: a refused end retried forever
   is a storm on a row no robot may touch. A stamp's refusal (exit 2, the
   matrix absent; exit 3, its bytes unverified) degrades the row as
   `STAMP_FAILED` and the row is never offered a stamp again, so it cannot
   storm; adding a different refusal event requires an explicit contract change in both tables.
12. <a id="adopt"></a>**It adopts what it did not make, without touching
   it.** Four kinds of work, one table in the poller and one in the
   governor: `stamp`, `reap`, `validate`, `adopt`. An adoption binds a
   ledger row to a container that already existed — named by the row's
   `instance` param, read by the recipe as `SHAPER_PARAM_INSTANCE` — and
   is a birth to the ledger, so it is proven like one: by the facts the
   recipe looked at (the container runs, `legacy: true`), never by an exit
   code; an adopt recipe that ends without a line of facts is reported
   `ADOPT_FAILED`. The recipe looks and reports; it creates nothing,
   launches nothing, and never exec's inside the container it adopts: a
   frozen tenant is frozen. The constructor authors the class’s adopt recipe and qualifies it on the selected host before enabling adoption.

## 3. Cognition

The maker is a robot: the recipe needs no judgment. An agent may accompany it
to watch and to report anomalies — that agent has **no** hand on the host.

- **capacity-class**: none required for the recipe
- **role**: the accompanying watcher `requires` D1 / T1
- **degradation**: an unclear situation is reported and stops the job; it is
  never resolved by improvisation

## 4. Realization and dependencies

The constructor generates the maker implementation, manifest and frozen recipes in the separate realization. Its manifest declares mandatory alerting: silence must be heard. Recipes are selected by the class's shape and enrolled machine's host family (`proxmox`, `lxd`, `liblxc`, `nested`); a machine can offer several families, at most one per shape. No existing recipe or registry is a prerequisite to author one.

A frozen recipe may be a script in any suitable language or a compiled executable. The `.sh` naming convention applies only to the shell realization. Every realization preserves the same six positional arguments, fresh allow-listed environment, observed facts and exit-code meanings; language choice does not relax that protocol.

The maker's operational records and credentials have its own private MariaDB/secret boundary under the functional-unit contract. Host power stays at this parent level, never in a child or governor ledger. An authorized DEV lead agent may construct and qualify the maker; that does not turn the deterministic maker itself into an improvising cognition agent.

The exact protocol/state table is in [governor](governor.md), the argv, facts and exit codes in [maker recipes](maker-recipes.md), and host shapes in [Rule 11](../../RULES.md#rule-11). [Fleet](../architecture/FLEET.md) defines placement; [Rule 36](../../RULES.md#rule-36) defines parent SSH authority.
