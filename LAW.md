# SHAPER OS V1.15 — Operational Law

This repository contains the complete governing documentation for constructing V1.15 realizations and for continuing development in projects that explicitly adopt its standard. Read [RULES](RULES.md) in full, the [boot contract](docs/agent/BOOT-CONTRACT.md), and the affected contracts in the [governing map](docs/GOVERNING-CORPUS.md). No separate SHAPER release is needed.

The rulebook consists of the [rule index and all seven canonical parts](RULES.md#complete-rulebook).
Reading the index alone does not satisfy full rule reading; the complete rule
bodies in every part retain their binding force.

## Two uses and explicit adoption

SHAPER OS supports both constructing universes and their units, and governing
development within an existing project.

Reading or receiving this corpus alone does not authorize converting a project
into a SHAPER universe. When the human explicitly adopts SHAPER OS as the
project's development standard, however, it becomes the governing reference for
design, implementation, changes and evidence within the declared scope—not
optional background material. Record that adoption and continue ordinary
authorized development without requesting approval again for work already
covered by the mandate.

All obligations whose subject and conditions apply to that scope are binding.
Distinguish cross-cutting development obligations from contracts tied to a
declared architectural role, composition or realization profile. Non-applicability
follows from the actual subject and scope; it is not an exemption chosen for
convenience.

Adopting the development standard does not, by itself, declare every project
component to be a universe or functional unit. Conversely, an existing component
declared as a SHAPER universe or unit retains its applicable architectural,
storage, lifecycle and proof obligations. A project-scoped adoption cannot
silently waive them.

Record existing conformity gaps, their consequences and the authorized
correction scope. A gap is neither compliance nor permission to weaken the
contract. Adoption does not authorize an unrelated migration or wholesale rewrite.
Resolve a genuine scope or authority conflict before its dependent action while
continuing independent authorized work.

## Operational obligations

1. The human–agent tandem owns the mission, role and jurisdiction. Knowledge of the frame grants no additional authority. Apply its explicit mandate and the recorded [current decisions](decisions/2026-10-06-SELF-CONTAINED-CORPUS.md).
2. This OS contains intent and contracts, not implementation. The constructor generates missing code, tests, image recipes and concrete unit contracts in a separate realization workspace. No pre-existing image, codebase or registry is required.
3. Native tests pass from a fresh realization checkout before images are qualified. Run the real unit and integration/acceptance tests after boot. A failing check is repaired before the dependent promotion; never hide it with a stub or fabricated success.
4. Start construction in DEV. Rebuild TEST from a blank system-container universe and fresh source, verify the complete affected workflow, preserve evidence and destroy its disposable state. Production remains durable and separately authorized.
5. Preserve the nested containment, per-functional-unit private MariaDB and Podman-only rules. Reuse a qualified brick by a declared source/digest reference, not an untracked copied implementation. When none exists, construct it.
6. Helm is the human interface: text and voice, bounded by jurisdiction and validated pilot level. Its console remains in architecture perimeter P2; business tools remain distinct P3 applications. These are layer names, not host identifiers.
7. The acting agent receives a prepared role-specific context and current evidence. The constructor understands the whole foundation; a runtime task does not carry the entire design corpus as its prompt. Session continuity never replaces an action ledger.
8. The parent repairs or reconstructs the child; an agent does not replace its own live vital infrastructure. The authorized maker holds its host/child SSH authority; no private key descends into a child or enters the governor's ledger.
9. Qualify typed deliverables through actual effects and independent observations. Code passing tests, a deployed artifact, a working live path and human acceptance are distinct evidence.
10. Promote by the canary protocol. Repairs are bounded; a failed component rests `DEGRADED` and escalation is observable. A resolved defect produces a regression test and an improved owning intent.
11. Secrets never enter tracked files, chat transcripts, public provenance or backup archives beside the key that opens them. Validate required credentials before their dependent operation and continue other authorized work.
12. Design security boundaries from the outset. Implement necessary functional/perimeter protections during DEV while the tandem actively directs construction. After integrated functional acceptance, harden the complete system and verify the accepted workflows under the production action/type permissions. Do not invent repeated approvals inside an already approved envelope.
13. Speak French with the operator and write technical artifacts in English. Human-facing business answers use plain language; technical evidence remains inspectable.

A summary, navigation page or prior reading claim does not replace full reading. The [perimeter taxonomy](docs/architecture/PERIMETERS.md), [consulted-context doctrine](docs/design/CONSULTED-CONTEXT.md) and specialist contracts preserve the detailed obligations. Existing deployments are not modified by publishing these documents; any later change to them has its own mandate and qualification.
