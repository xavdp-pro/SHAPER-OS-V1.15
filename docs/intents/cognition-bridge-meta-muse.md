# Realization intent — Meta Muse cognition bridge

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)
> **Scope**: Reusable Meta Muse adapter profile; concrete universe bindings belong to its realization.

Identifier: **REALIZATION-BRIDGE-META-MUSE**.
Status: **[TARGET]** optional adapter profile applying the
[generic bridge intent](cognition-bridge.md), under the
[6 October clarification](../../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md).
The common intent owns mission, authority, context, continuity, effects and evidence.
Provider-specific execution belongs to this profile and its separate realization.

## Function and variants

Expose Meta Muse cognition for bounded jobs through the common bridge role.
Declare whether the realization uses a CLI with tools or a conversation API.
These are different execution capabilities. Do not describe an API-only adapter
as a CLI executor, or infer shell/SSH capability from a fluent answer.

The source comparison on 6 October 2026 found an API adapter that replays stored
conversation messages and a current system instruction; it has no vendor-native
session and no local tool-execution loop. Its local history is bounded and only
successful turns join that history. The older CLI-oriented intent described a
different realization target, not the capabilities of that API implementation.
This is a source observation, not a current provider-service or runtime test.

## API realization

Map the logical session to owned conversation state, with current context and
explicit replay. Preserve context revisions and session/run identity; declare
history retention and detect when reconstruction is needed. Reload the owning
unit's action and evidence records before each task. A successful-history-only
transcript cannot establish that a failed or interrupted external operation had
no effect.

Declare text generation and any actual tool capability separately. If actions
are performed by another authorized Runtime executor, specify the proposal,
authorization, execution, check and feedback relationship. Otherwise qualify
this adapter for analysis/output only. Do not pretend it performed shell commands,
handled a mailbox or changed a remote system.

Under the current construction profile, the bridge's authoritative durable
conversation/context metadata belongs in its private MariaDB. JSON-file history
in an existing prototype is an implementation gap to migrate and restore-test,
not an exception to the profile or a silent migration of a running deployment.

## CLI realization, when selected

The realization repository owns the executable, supported version, stream
translation, native session mapping or replay, and tool-permission controls.
For mandated DEV, provide full execution without a CLI sandbox, blocking approval
or user-input prompt, following the
[common execution policy](cognition-bridge.md#execution-policy-for-mandated-development).
Qualify explicit timeout/spawn failure and the actual tool/network capabilities
within the agreed jurisdiction. A flag documents a mechanism; the run evidence
establishes whether the authorized action was possible and completed.

Old CLI flags, sandbox behavior and credential names are lineage to verify on
the actual supported version. Do not prescribe them as timeless generic law.
A CLI realization must prove the same common context and recovery lifecycle as
the API variant, including changed context on resume and lost-session recovery.

## Production action policy

Apply the [common production policy](cognition-bridge.md#production-permissions-per-action-or-action-type)
decided and implemented by the human–AI tandem for each action or action type.
For an API-only adapter, the authorized executor enforces the action permissions;
for a tool-capable CLI adapter, its Runtime/tool integration enforces them.
A schedule or queued task stays within that policy, without repeated approval
for actions it already covers.

## Configuration and acceptance

The realization declares its API endpoint or CLI, credential references,
model selection, listener/port, caller authentication, workspace where relevant,
state ownership, limits, concurrency and terminal-event semantics. Do not fix a
provider model or deployment port in the agnostic frame. Fail clearly when an
actual required capability or credential is absent; simulated tests are labeled
and do not qualify real cognition.

Apply the [common acceptance questions](cognition-bridge.md#qualification-questions).
Prove session/context continuity, refresh, reset/reconstruction and restart/restore
for the selected variant. Verify an actual authorized effect only when its
declared executor supports that action. Keep optional adapter failure independent
of the four base units. Code, images, tests and deployment material stay outside
this OS repository; no implementation repository is required to read this intent.
