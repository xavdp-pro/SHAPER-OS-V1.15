# Human reading guide — five depths

The five depths preserve V1.14's existing human route. They describe what a
reader wants to understand, not their value, rank or permissions. A person may
move between them. Begin with the [board's orientation](../CONTEXT-INDEX.md),
then use the depth below that answers your question. The learning chapters are
available now; detailed-law reconciliation remains open in the
[ledger](../../review/READING-LEDGER.md).

The inherited labels Owner, Operator, Engineer and Architect name reading
perspectives, not appointments or permission grants. You may read a subset;
principal agents must read the complete study set. Each chapter starts with a
short plain-language explanation so introductory readers can understand the
whole shape without first reading every operational detail.

## Level 1 — Owner: understand the purpose

Start with a real situation: a supplier changes prices and old quotations must
remain correct. The human explains the desired result; the authorized owner
decides which changes the agent may perform. Reading at Level 1 grants neither
ownership nor authority. SHAPER supplies a way to preserve that meaning, check the
outcome and learn from discrepancies.

Read [Intent](../../INTENT.md) and
[chapter 1](../learning/01-INTENTION-AND-GOVERNANCE.md). Explain what stays under
your control, what the agent is expected to produce and what counts as success.
Practice C8 in the [scenarios](../examples/COMPREHENSION-CHECKS.md): repeated
success does not silently grant permission for permanent automation.

## Level 2 — Operator: understand everyday operation

Follow an agreed action from request to result. A recurring price update needs
an owner, a schedule if recurring, the correct input, an observable result and
a way to recover when a supplier message is missing. Seeing an acknowledgment
does not prove the prices were correctly updated.

Read [chapter 4](../learning/04-UNITS-AND-DEPENDENCIES.md) with its prerequisites
and [chapter 6](../learning/06-EVIDENCE-RECOVERY-LEARNING.md). Ask who notices
silence, where evidence lives and how to stop or amend an existing mandate.
Practice C2 and C7. Explain why “the service is up” does not establish that the
price update worked. You need not learn the implementation language to do this.

## Level 3 — Engineer: understand realization obligations

Read [the vocabulary boundary](../architecture/VOCABULARY-BOUNDARY.md). An intended
function receives a concrete implementation in a separate repository. Its
dependencies, state ownership, failure behavior and tests must be explicit.
Delivering an executable is only one part of delivering the required behavior.
Read [chapters 3](../learning/03-CREATION-EXECUTION-PROTECTION.md),
[4](../learning/04-UNITS-AND-DEPENDENCIES.md),
[5](../learning/05-MATERIALIZATION.md),
[6](../learning/06-EVIDENCE-RECOVERY-LEARNING.md) and their prerequisites. Practice C1, C4
and C5. Explain where state survives, why retry is not automatically safe, and
which documents the concrete realization needs before deployment.

## Level 4 — Architect: understand relationships

Trace what a change affects beyond its local component. A price import touches
historical quotations, permissions, stored events, notifications and downstream
calculations. Each boundary needs an owner and a contract. Strong reasoning does
not create authority, and an interface does not become the source of truth.

Read [chapter 2](../learning/02-LAYERS-AND-SCOPES.md) and the complete common
sequence. Practice C3 and C6. Explain the distinct containment, authority,
dependency, data and hosting relationships; changing one can affect the others
without making them identical.

## Level 5 — Systemic perspective: understand evolution

Examine how a pattern can recur at several scales while preserving local
boundaries. Useful autonomy includes the ability to perceive an error, stop,
seek another view and revise. Replacement of code preserves data and agreements
through verified migration. Repetition of a successful action alone does not
create a permanent mandate.

Read the complete common sequence, the
[source map](../../review/SOURCE-MAP.md), and
[self-checks](METACOGNITION.md). Revisit C5 and C7 from the perspectives of the
unit, universe, containing space and affected humans. Ask whether a local gain
damages the whole, and whether the mechanism intended to detect that damage is
itself observable. Source provenance makes this reasoning inspectable, not
infallible.

## Teaching method for every important concept

Define the words, advance in understandable steps, then reconnect to reality.
Every completed concept explanation answers five questions: what is it; why does
it exist; what happens in a concrete case; what can fail; how can we verify it?

Use the same example across depths so the reader can connect everyday experience
to the deeper structure. Understanding is demonstrated when the reader can
explain a decision or handle a new case, not merely repeat the vocabulary.

See [worked answers](../examples/WORKED-ANSWERS.md) for the same failure explained
at human Level 2 and medium-agent depth. Use the scenario rubric to check actual
understanding rather than treating vocabulary repetition as qualification.

This repository's technical reference text remains English. Human-facing wiki
explanations may present the same meanings in French without creating different
laws. A translation must preserve limits, unknowns and maturity labels, not only
the attractive parts of the explanation.
