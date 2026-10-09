# SHAPER OS V1.15 — shape what comes next, with AI agents

**SHAPER OS V1.15 is ready for use.** Its creator uses it every day to create,
deploy and organize universes, including nested Podman deployments.
The [6 October clarification](decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md)
records that practical experience and the scope of new-candidate qualification.

SHAPER OS gives humans and AI agents a shared framework for turning intentions
into systems that fit real needs. It connects purpose, responsibilities,
relationships, action and learning, while leaving room to improvise, explore
and discover possibilities that have not yet been imagined.

The human remains in command. Agents expand the ability to think, build and
explore. Different perspectives reveal new possibilities and help improve the
work. The framework grows through that practical experience.

## Discover the ideal scene

An entity has an adaptable **space**, composed of **universes** suited to its
activity. **Helm** lets the human pilot those universes within their jurisdiction.
Governors coordinate creation work and makers carry it out. Functional units
provide the capabilities of each universe, with clear responsibilities and
relationships.

This pattern can recur at different scales: that is its **fractal** expression.
Common principles support a diversity of compositions, activities and ways of
working.

Read [the ideal scene and first exercise](docs/IDEAL-SCENE.md), then try the
method with an agent on a situation that matters to you.

## Choose your entrance

To begin building, give a capable agent this repository and a simple request:

> Create a SHAPER OS universe called univ-example locally using Podman.

**The agent writes the implementation from the documented intentions and
contracts.** This repository is self-contained and deliberately code-free: its
[LAW](LAW.md), [RULES](RULES.md), boot and unit contracts are all present here.
You need neither another SHAPER OS edition nor an existing implementation.
Read the [local operational corpus](docs/GOVERNING-CORPUS.md#mandatory-local-operational-corpus).
The [rulebook](RULES.md#complete-rulebook) has seven shorter canonical parts
to support complete reading through bounded agent tools; all parts remain required.
See the
[starting requests and prerequisites](docs/examples/CREATE-A-UNIVERSE.md).

- Human readers: [five reading depths](docs/human/READING-GUIDE.md).
- AI agents: [agent entrance](AGENTS.md) and [ordered reading board](docs/CONTEXT-INDEX.md).
- Purpose and evolution: [intent](INTENT.md).
- Words and relationships: [glossary](docs/GLOSSARY.md) and
  [brick, package and functional unit](docs/architecture/VOCABULARY-BOUNDARY.md).
- Learning through practice: [self-checks](docs/human/METACOGNITION.md),
  [comprehension exercises](docs/examples/COMPREHENSION-CHECKS.md) and
  [worked answers](docs/examples/WORKED-ANSWERS.md).
- Building a reference universe: [construction procedure](docs/procedures/01-REFERENCE-UNIVERSE.md)
  and [current realization profile](docs/profiles/SEPTEMBER-CONTAINER-MARIADB.md).
- Asking an agent to create a universe on your machine:
  [a concrete starting request](docs/examples/CREATE-A-UNIVERSE.md), locally or
  over SSH, with Podman or LXC hosting.

## An enduring framework, evolving realizations

This repository carries the framework in English: intentions, principles,
contracts, explanations and examples. The agent creates concrete code, tests
and deployment material in a separate realization workspace. Existing code can
be reused when appropriate; it is optional. As agents and tools improve, new
realizations can preserve what matters while improving how it is achieved.

After a universe or its units have been built and verified, a registry is
recommended for reproducible reuse and duplication. It can come later; see the
[first-construction direction](decisions/2026-10-05-FIRST-CONSTRUCTION-AND-REUSE.md).

V1.15 is usable today and remains open to improvement. The
[governing corpus](docs/GOVERNING-CORPUS.md),
[reading contract](docs/READING-CONTRACT.md),
[source map](review/SOURCE-MAP.md) and
[editorial ledger](review/READING-LEDGER.md) make its evolution traceable.
The [practical-use direction](decisions/2026-10-02-PRACTICAL-USE-AND-REFERENCE-SCENE.md)
records this presentation and daily use.

## Conception dialogues & cognitive grounding dataset

For research teams and organizations seeking deeper agent alignment and contextual discernment, SHAPER OS provides an acculturation methodology grounded in its conception dialogues.

Analyzing this dialogue corpus alongside **SHAPER OS**, **SHAPER Three Layers**, and **PodMesh** makes the underlying rationale, human intent, and operational lessons available to agents. This grounding aims to reduce literalist rigidity and goal-hijacking (*specification gaming*) and support informed counter-review. Its effect must be evaluated for the actual agent and context; it is not a behavioral guarantee. These optional research materials are not prerequisites for using the self-contained SHAPER OS corpus.

The complete corpus of historical conception dialogues is available upon request:  
📧 [xavier@xavdp.pro](mailto:xavier@xavdp.pro)

## Explore the ecosystem

- [SHAPER Three Layers](https://github.com/xavdp-pro/shaper-three-layers): OS,
  Runtime and Workspace.
- [PodMesh](https://github.com/xavdp-pro/podmesh): container management for concrete
  realizations.
- [RARMURE](https://github.com/xavdp-pro/RARMURE): Real-Time Fractal Vibe Coding,
  currently in concept formalization and proof-of-concept preparation.
- [Public site](https://xavdp.pro/en/shaper-os): SHAPER OS and its intended experience.

### RARMURE proof of concept preparation

**Project status as of 7 October 2026: concept formalization and preparation of a proof of concept.**
RARMURE proposes parallel software exploration through separate virtual working
views, semantic references, multiple model/provider routes, complementary
counter-reviews, and evidence-based master selection. Its
[short and detailed explanation](https://github.com/xavdp-pro/RARMURE/blob/main/PROJECT-EXPLANATION.md)
preserves the design and its open questions.

The specifications and illustrations are published. No RARMURE application,
working plugin, runtime qualification, or measured speed gain is established.
The proposed first proof of concept is a bounded case with two workers on one
interacting behavior, fixed candidates, counter-review, and combined validation.

SHAPER inspires the treatment of intention, authority, evidence, correction,
and learning. RARMURE can function independently: no SHAPER installation or
service is a prerequisite. This ecosystem entry records an exploratory project,
not a required SHAPER component, a formal adoption of this corpus, or a change
to SHAPER OS V1.15's **ready-for-use** status.
