# Realization intents (declarative only)

Status: explanatory contracts for **implementations outside SHAPER OS**.

SHAPER OS V1.15 carries **intentions, obligations and verification questions** —
not packages, bricks, container recipes or bridge server code. See
[repository boundary](../../INTENT.md) and
[23 September decision](../../decisions/2026-09-23-AGNOSTIC-NO-CODE.md).

A **realization intent** here describes:

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
