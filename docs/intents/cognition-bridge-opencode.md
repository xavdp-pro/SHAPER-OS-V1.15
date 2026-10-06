# Realization intent — OpenCode cognition bridge

Identifier: **REALIZATION-BRIDGE-OPENCODE**.
Status: **[TARGET]** adapter contract applying the
[generic bridge intent](cognition-bridge.md). Its default place in the reference
composition is **[MANDATE]** under the
[24 September decision](../../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md).
This document states what to build and qualify; it is not implementation code
or a certification of the currently available adapter.

## Function and scope

Translate bounded SHAPER cognition work into OpenCode engine sessions, retaining
the mission, context, jurisdiction and evidence lifecycle owned by the common
intent. OpenCode is the selected adapter for this reference, not a universal OS
law. Vault, Logger, Queue and Maestro continue their own work when it is unavailable.

The realization supplies OpenCode and its dependencies inside the bridge runtime
or through another declared integration. A binary need not already exist on the
construction host. Record a supported engine version and make model/provider
access and credentials explicit before a real run. Do not copy a model name,
port or authentication assumption from an old deployment into a new one.

## Session and context contract

Map a stable SHAPER logical session to the OpenCode native session and its
workspace. Prepare context before the first task; apply current context and
changed instructions on later tasks; reload the owning unit's action record.
Persist the mapping, context revision, continuity status and run/evidence links.
The current construction profile requires the bridge's own private MariaDB for
its authoritative application state; identify and preserve any additional
engine-owned session store under the applicable storage contract.

If a native session is missing, a replacement must load reconstructed context
and reconcile pending/uncertain effects before new actions. A recreated session
with only the latest one-line prompt does not fulfill continuity. Workspace
changes, reset, context truncation and engine restarts use the same rule.

## Concrete transport to specify in the realization

The current adapter lineage uses an OpenCode server, native session creation,
asynchronous prompts and a translated event stream. These mechanisms are a
realization choice; qualify the installed version's actual behavior.

| Concern | Required realization detail |
| :--- | :--- |
| Public control surface | Versioned health/status, inject, correlated events, stop/reset, session/context preparation and metrics; map the generic obligations to exact routes and wire fields. |
| Engine mapping | Creation/reuse of native sessions, workspace scoping, prompt/context delivery, event correlation and loss detection. |
| Configuration | Listener address/port, engine executable/server address, supported version, model/provider selection, credential references, workspace roots, timeouts, storage and evidence limits. |
| Authentication | Caller identity and allowed operations; scoped engine/tool credentials. Exposing a listener never grants a mandate. |
| Headless execution | Authorized actions finish or fail explicitly without an unattended approval prompt; permissions remain bounded by the mission and Runtime controls. |
| Concurrency and stop | Serialize or reject conflicting session work; reconcile interrupted effects and retain terminal ownership. |
| Durable state | Private MariaDB bootstrap, context/session mapping, restart, backup and restore; declared engine state dependencies. |

For mandated DEV, configure full noninteractive execution with no CLI sandbox
or repeated permission prompts, as required by the
[common execution policy](cognition-bridge.md#execution-policy-for-mandated-development).
Map OpenCode permissions to that policy and the agreed workspace, credentials
and jurisdiction; a wildcard setting alone does not describe those boundaries.
A missing engine, model, credential or required capability
is reported as unavailable; no stub or successful health response substitutes
for a real run and observed effect.

## Production action policy

Apply the [common production policy](cognition-bridge.md#production-permissions-per-action-or-action-type)
chosen and implemented by the human–AI tandem for each action or action type.
Translate it into actual engine/tool/resource permissions before dispatch and
execution; Maestro and Queue do not broaden it. Qualify that enforcement and
the expected effect. A wildcard DEV setting is not the production configuration.

## Implementation gaps are explicit

The source comparison on 6 October 2026 found a native session-based adapter with
workspace binding, attachments and asynchronous event translation, but without
a dedicated context-registration/delivery contract. Missing native sessions were
recreated, and session metadata used a JSON file. These observations identify
work to reconcile with the common continuity intent and private-MariaDB profile;
they do not prevent a new implementation being generated from this contract.
The source comparison is not a live runtime qualification of any deployment.

The realization must publish a versioned interface document and tests for its
actual implementation. The OS does not prescribe arbitrary fixed ports, variable
names or provider models to fill an implementation gap.

## Acceptance

Apply all [common qualification questions](cognition-bridge.md#qualification-questions).
For this adapter additionally prove native session reuse in the correct workspace,
context revision changes, loss/reconstruction, durable restart/restore, an
allowed real tool action with independent effect evidence, and a refused
out-of-perimeter action. Verify that a cognition outage leaves base units usable.
Record source checks, installed configuration, engine run, effect verification
and human acceptance separately. Construction of independent base units continues
while a missing cognition dependency is resolved; the full reference is qualified
only when all its declared requirements pass.
