# Realization intents — ready-to-implement contracts

A **realization intent** states what an external realization must provide so it
can be built, qualified and replaced against a stable meaning. SHAPER OS V1.15
carries the **intentions, obligations and verification questions** for that
purpose; packages, bricks, container recipes and bridge server code live in
their own repositories — see [repository boundary](../../INTENT.md) and the
[23 September decision](../../decisions/2026-09-23-AGNOSTIC-NO-CODE.md).

Each intent here describes:

- what function the realization must provide;
- how it relates to generic cognition-bridge obligations (optional adapter);
- what must never block unattended operation when the human is absent;
- what evidence proves the realization is working;
- where executable artifacts are expected to live (separate repositories).

Implementations may change every month; these documents must remain stable enough
that a replacement can be qualified against them.

## Index

| Intent | Role |
| :--- | :--- |
| [Meta Muse cognition bridge](cognition-bridge-meta-muse.md) | Headless adapter — implementation: [xavdp-pro/muse-bridge](https://github.com/xavdp-pro/muse-bridge) |

Historical executable references (V1.14 `pkg-bridge-*`, external GitHub bridges)
are **lineage and comparison material**, not imports into this repository.
