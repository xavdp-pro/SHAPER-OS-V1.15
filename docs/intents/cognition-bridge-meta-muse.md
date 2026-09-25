# Realization intent — Meta Muse cognition bridge

Profile identifier: **REALIZATION-BRIDGE-META-MUSE**  
Status: adopted intent for external implementation; not an executable artifact in SHAPER OS.  
Lineage: V1.14 agent-bridge practice (Rule 8 HTTP/SSE), measured CLI contracts in
`doctrine/AGENT-CLIS.md` (V1.14 reference tree), operator requirement for
**no sandbox cage, no blocking CLI prompts, always responsive** headless runs.

## Applicability

Use this intent when a **realization** (not SHAPER OS itself) must expose the
Meta Muse CLI to Maestro, Queue or Helm through the same **cognition-bridge**
role described in the
[September target profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md): an optional
adapter for bounded cognition jobs. The base socle must remain runnable without it.

SHAPER OS does **not** host the server code. A separate realization repository
owns the bridge process, tests, container image and deploy hooks:

**https://github.com/xavdp-pro/muse-bridge** (public), analogous to
`cursor-bridge` / `opencode-bridge` adapters outside the agnostic corpus.

## Function

The bridge translates a stable HTTP control plane into one-shot or session-bound
Muse CLI runs inside a declared workspace perimeter. Callers inject work; the
bridge streams progress and terminates with an explicit outcome. Swapping Muse for
another engine must not require structural changes elsewhere—only the adapter and
its measured model variable.

## Interface obligations (generic cognition bridge)

The realization MUST expose, at minimum:

| Surface | Obligation |
| :--- | :--- |
| Health | Report whether the process is serving and whether required credentials and model configuration are present (without naming a default model). |
| Inject | Accept a conversation key, message, optional context file path, optional perimeter path; start one run; return a run identifier immediately. |
| Events | Server-sent events: connected, start, streamed agent output, log lines, terminal `done` with exit code. |
| Vitals | Publish operational evidence (counts, in-flight runs, CLI reachability); must not claim a single boolean “healthy” verdict without evidence fields. |

Authentication between caller and bridge is realization-specific (Bearer token,
mesh identity, or localhost bind). The intent requires **some** declared auth when
not bound to loopback only.

## Meta Muse CLI obligations (unattended)

Default Muse CLI behavior is unsafe for unattended deployment: approval prompts,
sandbox network `proxy-only` (breaks SSH and remote tooling), and silent blocking
on user-input tools.

Every **real** run the bridge spawns MUST satisfy all of the following, verified
on the target host by hand at least once before production trust:

1. **Full auto approval and sandbox off** — Muse documents `--yolo` as disabling
   approval and sandbox for the run. Implementations MUST use this (or an
   equivalent documented combination that measurably achieves the same on the
   installed CLI version).
2. **No blocking user-input** — Headless runs MUST auto-resolve or cancel
   `request_user_input` (Muse: `--user-input-auto-resolve`).
3. **Machine-readable stream** — stdout MUST use Muse JSONL (`--json`) so the
   bridge can forward typed events without guessing from plain text.
4. **Non-interactive child environment** — Git, npm, pip, debconf and similar
   MUST not read the tty (CI-style env: no terminal prompts).
5. **Spawn failure is a run outcome** — A missing binary or refused start MUST
   end the run on the event stream and MUST NOT crash the bridge process serving
   other conversations.

The bridge MUST NOT rely on exit codes alone as proof of success; witness streamed
events and explicit error payloads.

## Configuration obligations (measured, not pinned in SHAPER OS)

| Variable | Tier | Meaning |
| :--- | :---: | :--- |
| `MUSE_MODEL` or `META_MUSE_MODEL` | required when not in stub/simulation | Engine id **measured** on the deployment host (same discipline as other bridges; no default in OS or bridge source constants). |
| `META_API_KEY` or `META_MUSE_API_KEY` | required for real runs | Provider credential for `muse exec`. |
| `MUSE_BRIDGE_PORT` | realization default | Convention **4320** in current P2 lineage; universes may override if documented. |
| `BRIDGE_MUSE_STUB` | test only | Simulated bridge without spawning CLI. |

Optional: `MUSE_PROVIDER`, `MUSE_REASONING_EFFORT`, `MUSE_HOST_BIN` (host-mounted
CLI path in container realizations), shared `WORK_ROOT` for perimeter enforcement.

## Cognition declaration (Rule 21 vocabulary)

- **capacity-class**: `heavy-engineering`
- **role**: provides (adapter)
- **depth**: D3
- **throughput**: T2
- **degraded**: allowed-with-note when API or CLI is temporarily unavailable

## Deployability (realization repository)

Before a universe enables this adapter, the realization MUST document and prove:

- how the Muse binary enters the runtime (mount, image layer, or sidecar);
- how workspace and perimeter paths align between host and container;
- halt behavior when model or API key is missing (fail closed with readable message);
- SSE behavior under concurrent injects per conversation key;
- evidence artifact from one successful headless run that performs a required
  remote or shell action (not merely “process still alive”).

## Explicit non-goals for SHAPER OS V1.15

- No `@shaper/pkg-bridge-muse`, no `brick-bridge-muse`, no `server.js`, no
  Podman recipes in this repository.
- No new default model id or provider ranking in OS text.
- Experimental code landed in **SHAPER-OS-V1.14** on branch
  `cursor/pkg-bridge-muse-headless` is **comparison material only**; do not
  treat it as successor law or merge it into V1.15. Prefer a dedicated external
  realization repo qualified against this intent.

## Verification questions (comprehension)

1. Why is `--yolo` insufficient as the only proof that SSH from Muse succeeds?
2. What observable proves a run finished vs. the bridge HTTP process still listening?
3. Where must `MUSE_MODEL` be chosen, and what fails if it is copied from a doc?
4. What breaks if implementation code is added to SHAPER OS V1.15?

Compare [materialization](../learning/05-MATERIALIZATION.md) and
[vocabulary boundary](../architecture/VOCABULARY-BOUNDARY.md).
