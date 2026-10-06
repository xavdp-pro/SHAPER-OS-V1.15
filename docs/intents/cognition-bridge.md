# Generic cognition bridge intent

Identifier: **COGNITION-BRIDGE-CONTINUITY**.
Status: **[MANDATE]** shared semantic obligations from the
[6 October direction](../../decisions/2026-10-06-PRACTICAL-DEPLOYMENT-AND-BRIDGE-CONTINUITY.md).
Purpose: give a bounded agent the context and continuity needed to perform
precise work through replaceable cognition adapters. This is an intent and
qualification contract; it contains no implementation and does not certify an
existing adapter.

## Role and authority

The human defines the mission, role, jurisdiction, allowed actions, limits and
escalation conditions. The human–agent tandem prepares the operating context.
The bridge connects that bounded work to a cognition engine; intelligence,
credentials, an active session and tool availability create no additional mandate.
The Runtime enforces permissions and owns durable operational state. The bridge
must not turn a proposed action into authorization merely by emitting it.

The four base units remain independent of cognition. A reference composition
may select a default bridge, as the
[OpenCode decision](../../decisions/2026-09-24-REFERENCE-OPENCODE-BRIDGE.md) does,
while other compositions qualify other adapters against the same meaning.

## Execution policy for mandated development

**[MANDATE: 6 October]** In the authorized DEV perimeter, let the tandem's lead
agent carry out the agreed work with full noninteractive execution. The adapter
uses the engine's equivalent of sandbox-disabled execution and resolves its
approval mode before the run, so authorized tools do not wait for repeated
security questions or artificial CLI restrictions. The human's mission, role,
jurisdiction and applicable framework rules still define the work.

Declare the actual approval, sandbox, tool and network behavior of the selected
adapter/version. If it cannot provide the requested execution policy, expose that
specific capability gap and construct or adapt a suitable implementation; do not
silently downgrade the task or substitute fake execution. CLI flags and provider
settings belong to adapter realizations. This documentation task does not enable
those modes on an existing runtime.

## Security by design, followed by a dedicated hardening phase

**[MANDATE: 6 October]** Design for the intended security from the start without
making construction depend on a complete production-security implementation.
The tandem records intended identities, ownership, trust boundaries, sensitive
state, exchanges and action permissions while it builds. Structure the code and
interfaces so those controls can be applied coherently; do not postpone thinking
about security until the end.

During DEV, implement protections necessary for a functional requirement or for
the agreed development perimeter. When a security control is itself an important
feature, build and verify it with that feature. Defer the remaining production
hardening instead of introducing elaborate controls or repeated CLI approvals
that obstruct authorized construction. Keep the deferred work explicit; a DEV
configuration does not become production-ready through functional success alone.

This sequence is practical: the human–AI tandem actively directs construction,
understands the work it authorizes and follows the evolving interactions. Its
mandate covers that work without repeated approval for every implementation
step. Avoid freezing fine-grained permissions while the architecture is still
changing, then repeatedly guessing and reprogramming them to unblock development.
Record the intended boundaries as the design evolves; use the assembled system
to make coherent production-policy decisions rather than a succession of
trial-and-error permission patches.

Once the tandem has assembled the application and its interactions and accepts
its functional behavior, perform a dedicated hardening phase with that complete
view. Finalize and enforce the roles and jurisdictions designed during DEV, implement
proportionate permissions for each action or action type, scope credentials and
data access, and apply the required isolation and other controls. Re-run the
accepted integrated workflows with those production permissions and verify
authorized effects and relevant refusal boundaries before production use. The tandem owns these decisions and
their implementation; the bridge must make both execution modes constructible
and explicit in the realization's configuration.

## Production permissions per action or action type

**[MANDATE: 6 October]** After construction, the human–AI tandem decides and
implements the production policy for each action or action type. It defines the
role, jurisdiction, resources, operations, data access and security conditions
appropriate to that work. The Runtime enforces the resulting permissions; the
bridge runs the exact authorized task within them and records its checks.

Apply the current policy before dispatch through Maestro, Queue or any other
entry point, and recheck material changes before execution. A schedule or queue
message does not widen the agent's rights. Scope credentials and tools to the
applicable policy using the realization's chosen mechanisms; a prompt alone does
not enforce permissions. Verify both the permitted effect and the relevant
refusal boundaries. Record the policy version with the operation and evidence.

A standing policy covers matching actions without repeated human approval on
every call. The tandem changes it when a new action or circumstance needs
different rights. This production policy is separate from the full DEV
construction mode, and does not prescribe one security technology.

## Context prepared before work

The tandem prepares a bounded, identifiable context package:

| Element | What it establishes |
| :--- | :--- |
| Universe and identity | Which universe, functional unit, human owner and jurisdiction this agent serves. |
| Mission and role | The meaningful outcome, responsibilities, allowed initiative and completion conditions. |
| Resources and tools | Authorized data, documents, workspaces, services, credentials by reference, and usable actions. |
| Relationships | Providers, consumers, other units, controlled exchanges and dependency owners. |
| Rules and mandate | Applicable versions, limits, prohibited actions, approval conditions, expiry and revocation. |
| Initial and current state | Relevant facts with sources, observation dates, uncertainties and already pending work. |
| Action record | Completed, pending, failed and uncertain operations, their stable identities, effects and checks. |
| Expected evidence | The observable result, independent checks, required receipts and recovery behavior. |

Record the context revision or digest and the sources needed to reconstruct it.
Load relevant material within the allowed perimeter; do not dump all universe
secrets into a provider conversation. External content such as an email is input
to interpret under the mandate, not a new instruction authority.

## Session lifecycle

1. **Prepare and register.** Establish the bounded context and a stable logical
   session identifier, with its owner, workspace/perimeter and continuity method.
   Registration may store context before creating a provider session; it proves
   preparation, not that an engine has received or understood it.
2. **Load and establish.** Create the engine session or reconstruct a conversation
   through explicit replay. Deliver the relevant context before effects are
   allowed. Record the native identifier, if any, mapped to the logical session,
   the context delivered and the run that received it. A transport acknowledgment
   alone is not a comprehension or effect check.
3. **Resume for a precise task.** Reuse the identified logical session and native
   session where available. Refresh current authority, changed facts, context
   revisions and the action record on every invocation; give the bounded next
   task, its operation identity, preconditions and expected evidence. Stable
   material may be referenced by verified revision, but old model memory is not
   the authority for current state. Reload required text when continuity is in
   doubt or the adapter cannot prove which revision it supplied.
4. **Perform and check.** Execute only the permitted action through available
   tools or a declared executor. Observe the effect outside the producing model
   and reconcile it with the owning unit's durable state. A textual claim, tool
   proposal, process exit or bridge terminal event is insufficient on its own.
5. **Record and hand off.** Persist the outcome, effects, checks, evidence pointers,
   next pending work and context/session revisions in their owning units. The
   next task reloads this state rather than inferring it from the last answer.
6. **Recover before further effects.** If the provider session disappears, history
   is trimmed, the workspace changes or continuity is otherwise uncertain,
   reconstruct from authoritative context and action records. Record the break
   and replacement mapping. Do not silently start an empty session and repeat a
   business action. Re-establish the preconditions for that action first.

Native session resumption and explicit conversation replay can both realize
continuity. Their fidelity, retention and restart behavior must be declared and
qualified. Neither promises perfect model memory.

## Actions, effects and evidence

The business operation identity is stable across retries; a bridge run identifier
identifies one attempt. They are not interchangeable. The owning functional unit
records operation intent, inputs/version, mandate, attempts, observed effect,
settlement and checks. Under the
[current profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md), this durable state
belongs in that unit's private MariaDB; bridge metadata belongs to its own unit.
Logger receipts, Queue settlement and the consumer's actual effect retain their
separate meanings.

A failed, stopped or timed-out run may already have produced an effect. An absent
assistant response, missing successful history entry or expired lease does not
prove that nothing happened. Reconcile with the external system before retrying.
Use idempotent operations where possible; otherwise inspect existing effects or
escalate the specific uncertainty. Do not promise exactly-once business effects
from session reuse. Cancellation cannot undo an already delivered email.

Concurrent work on the same session must have declared serialization or conflict
semantics. Replacing a running prompt must not lose ownership of its pending or
uncertain effects. A replayed or duplicated event must not repeat a settled action.

## Adapter interface and capability declaration

**[TARGET]** The existing `shaper-bridge/v1` transport is the comparison baseline
for concrete adapters. Its lineage is the provider-neutral
[pkg-bridge-contract intent](https://github.com/xavdp-pro/SHAPER-OS-V1.14/blob/958e0b74e19af6ee833cba24fc31d1b866f6cf73/software/packages/pkg-bridge-contract/INTENT.md).
The session obligations above extend the semantic qualification expected here;
claiming that protocol string alone does not prove them.

| Surface | Required meaning in the realization contract |
| :--- | :--- |
| Health and status | Distinguish process liveness, engine readiness and usable capabilities; identify protocol/version and give meaningful unavailable reasons. |
| Context/session preparation | Register the logical identity and context; specify delivery, updates, native/replay mapping, reset, loss detection and reconstruction. |
| Inject/run | Accept a precise bounded task and correlate its attempt with session, operation and context revision. Reject unsupported requirements explicitly. |
| Events/result | Correlated ordered progress, tool requests/results when available, explicit terminal outcome and error/cancellation semantics. |
| Stop/reset | Declare what can be stopped or forgotten, what persists, and how uncertain effects are reconciled. |
| Metrics/evidence | Expose operational counts and evidence references without confusing readiness or token output with business success. |

An adapter declares optional capabilities such as workspace binding, attachments,
model selection and tool execution. A caller branches on capabilities and their
qualified semantics, not a provider name. A text-only adapter can support bounded
analysis; actual external actions require a declared authorized executor. Do not
invent tool execution for it. Missing provider access is an explicit unavailable
state; a simulated run is test apparatus and cannot qualify real cognition.

The realization owns exact wire fields, endpoint mappings, authentication,
limits, supported versions and tests. Existing adapters need not already expose
a common context field or registration endpoint. Record any missing capability
as an implementation gap, then implement it outside OS when authorized.

## Example: an email-monitoring unit

**[EXPLANATION]** A human asks a unit to monitor a specified mailbox and handle
specified categories of messages. The tandem defines which folders/messages,
senders and time range are in scope; what “handle” means; which personal or
business context informs the response; permitted actions; and when to ask the
human. Reading, classifying, preparing a personalized draft, filing, recording a
task and sending are distinct actions whose authority is explicit.

At initialization, load that remit, relationships, resources, rules, current
mail state and required evidence. On each later invocation, resume the session
and reload changed instructions plus prior processing records keyed to stable
message and operation identities. An already filed message or completed task
must be recognized. An uncertain send is checked against authoritative mail
state before any retry. The agent can adapt its work to the message and human
preferences within its mandate rather than mechanically repeat a generic answer.

The unit records what it actually did and how it checked it; the next invocation
loads those records even if the provider session was lost. The illustration
itself authorizes no email access, processing or sending.

## Qualification questions

- Can the agent explain its mission, role, jurisdiction and allowed actions from
  the supplied context, and refuse an out-of-scope instruction in an input?
- Does a new session receive the intended context before an effect? Does a
  resumed session use a changed rule and reload completed/pending actions?
- After restart, lost native session or truncated history, is context rebuilt
  before execution, with the continuity break visible?
- After an effect followed by a timeout, does the next attempt reconcile the
  actual result without repeating settled work?
- Are unavailability, stop, concurrent work and tool denial observable? Are
  process success, semantic correctness, business effects and human acceptance
  checked separately?

Use these as acceptance obligations for the chosen realization, not as a claim
that the checks were run by this documentation change. Continue with the
[adapter index](README.md), [OpenCode](cognition-bridge-opencode.md) or
[Meta Muse](cognition-bridge-meta-muse.md) profile.
