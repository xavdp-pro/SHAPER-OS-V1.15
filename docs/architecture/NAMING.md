# Naming Contract

## Current vocabulary and source identity

Agent-facing texts name the functional part a **functional unit** (FUnit,
organelle) and human-facing texts a **component**, under the
[27 October vocabulary direction](../../decisions/2026-10-27-TECHNICAL-AND-CLIENT-VOCABULARY.md);
`brick-*` remains a compatible artifact prefix. [Composition](COMPOSITION.md)
separates class, specialization and instance; [source roles](SOURCE-ROLES.md)
separates mental/product/lab custody. The `univ-*` grammar below applies to that
identifier lineage, where “universe” keeps its earlier sense of one operational
composition. New source roles are not forced into `univ-*`; renames preserve
explicit link, submodule, import and image mappings. Repository names never
grant runtime identity.


> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Every identifier states its layer. Do not infer a layer from context.

| Prefix | Layer | Example |
| :--- | :--- | :--- |
| `univ-` | Operational composition of the `univ-*` lineage, usually a specialized cell class or instance | `univ-base` |
| `brick-` | OCI deployable definition | `brick-bridge-opencode` |
| `pkg-` | Reusable source package | `pkg-bridge-opencode` |
| `img-` | Registry image | `img-bridge-opencode` |
| `ctr-` | Running container role | `univ-base-ctr-bridge-opencode` |
| `vol-` | Persistent cell-owned volume | `vol-univ-base-vault` |
| `cfg-` | Configuration file or object | `cfg-univ-base.env` |
| `ctx-` | Agent context | `ctx-mail-triage.md` |
| `task-` | Declared unit of work | `task-mail-triage` |
| `proof-` | Evidence artefact | `proof-univ-base-<release>` |

A functional unit may exist at several layers. For example, `pkg-bridge-opencode`
is code; `brick-bridge-opencode` is the deployable OCI definition built from it; and
`img-bridge-opencode` is its immutable registry artefact. They are not synonyms.

**A layer must be earned.** In the realization, a deployable `brick-` has an actual build definition and can become a Podman image; source-only code is a `pkg-` package. This code-free OS describes those layers without carrying their code.

## Generic boundary

`pkg-agent-runtime` is generic. It dispatches a cell-declared `task-*` to one
selected `brick-bridge-*`; it knows no IMAP, SMTP, client, customer or business
workflow, and neither does `pkg-maestro`, which vendors it. A task carries a
`slug` and a cadence — nothing else is required of it, because requiring a
`label` and a `port` is how a monitored mailbox and its container port survived a
rename and stayed in the base. Mail intake belongs to catalogue `pkg-mail-agent`
and to the cell that declares the related `task-*`.

## Where a composition manifest states origin

A composition manifest of the `univ-*` lineage declares each functional unit’s `source`: `base`, `catalogue`, `fork` or `native`; `perimeter`: `P1`, `P2` or `P3`; and `forkedFrom` only for a fork. For example:

```json
"brick-vault": { "source": "base", "package": "@shaper/pkg-vault", "image": "img-vault", ... }
```

Nothing is inferred from a path. The realization validates every declared source. A generic base cannot silently depend on a private catalogue; put that composition in the appropriate class and declare its dependencies.

## The universe field and the repo name

For a **class repo using the compatible `univ-*` profile**, the manifest's `universe` field IS the class name and
matches the repository name exactly (`univ-mailo-core` in the repo
`univ-mailo-core`). Compositions living **inside the base** (`univ-base`, the
`_template`, test compositions) are not class repos — they keep their short
slugs and are exempt from the `univ-<project>-<class>` grammar, which binds
repositories, not in-base folders (Rule 1).

[Rule 1](../../RULES.md) owns source roles, compatible naming, immutable release slices and scoped fork mirror grammar. [Rule 37](../../RULES.md#rule-37) and the [lexicon](LEXICON.md) own lifecycle and lineage vocabulary.
