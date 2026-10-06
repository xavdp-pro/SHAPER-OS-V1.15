# Naming Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

Every identifier states its layer. Do not infer a layer from context.

| Prefix | Layer | Example |
| :--- | :--- | :--- |
| `univ-` | Deployable universe | `univ-base` |
| `brick-` | OCI service definition | `brick-bridge-opencode` |
| `pkg-` | Reusable source package | `pkg-bridge-opencode` |
| `img-` | Registry image | `img-bridge-opencode` |
| `ctr-` | Running container role | `univ-base-ctr-bridge-opencode` |
| `vol-` | Persistent universe-owned volume | `vol-univ-base-vault` |
| `cfg-` | Configuration file or object | `cfg-univ-base.env` |
| `ctx-` | Agent context | `ctx-mail-triage.md` |
| `task-` | Declared unit of work | `task-mail-triage` |
| `proof-` | Evidence artefact | `proof-univ-base-<release>` |

A component may exist at several layers. For example, `pkg-bridge-opencode`
is code; `brick-bridge-opencode` is the OCI service built from it; and
`img-bridge-opencode` is its immutable registry artefact. They are not synonyms.

**A layer must be earned.** In the realization, a deployable `brick-` has an actual build definition and can become a Podman image; a source-only component is `pkg-`. This code-free OS describes those layers without carrying their code.

## Generic boundary

`pkg-agent-runtime` is generic. It dispatches a universe-declared `task-*` to one
selected `brick-bridge-*`; it knows no IMAP, SMTP, client, customer or business
workflow, and neither does `pkg-maestro`, which vendors it. A task carries a
`slug` and a cadence — nothing else is required of it, because requiring a
`label` and a `port` is how a monitored mailbox and its container port survived a
rename and stayed in the base. Mail intake belongs to catalogue `pkg-mail-agent`
and to the universe that declares the related `task-*`.

## Where a universe states origin

A universe manifest declares each brick’s `source`: `base`, `catalogue`, `fork` or `native`; `perimeter`: `P1`, `P2` or `P3`; and `forkedFrom` only for a fork. For example:

```json
"brick-vault": { "source": "base", "package": "@shaper/pkg-vault", "image": "img-vault", ... }
```

Nothing is inferred from a path. The realization validates every declared source. A generic base cannot silently depend on a private catalogue; put that composition in the appropriate class and declare its dependencies.

## The universe field and the repo name

For a **class repo**, the manifest's `universe` field IS the class name and
matches the repository name exactly (`univ-mailo-core` in the repo
`univ-mailo-core`). Universes living **inside the base** (`univ-base`, the
`_template`, test universes) are not class repos — they keep their short
slugs and are exempt from the `univ-<projet>-<classe>` grammar, which binds
repositories, not in-base folders (Rule 1).

[Rule 1](../../RULES.md) owns the five repository kinds, immutable release slices and fork mirror grammar. [Rule 37](../../RULES.md#rule-37) and the [lexicon](LEXICON.md) own lifecycle and lineage vocabulary.
