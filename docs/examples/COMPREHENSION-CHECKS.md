# Comprehension checks — from words to a new situation

Status: documentation exercises, not executed runtime tests or deployment proof.
Prerequisites: [common sequence](../CONTEXT-INDEX.md) and
[self-checks](../human/METACOGNITION.md).
Sources: explanatory derivations from the chapters linked below. These fictional
examples add no adopted business policy; production choices need their owner.
Status labels: scenario prose and expected answers are **EXPLANATION**;
assessment procedures are **EDITORIAL**. Explicit target references do not
make their implementation choices universal law.

## The shared situation

A supplier changes its prices. The desired outcome is that new quotations use
validated prices from the agreed effective date, while already accepted quotes
retain their committed meaning. The human and agent first clarify responsibility,
inputs, authority, exceptions and proof. No specific database or language is
needed to understand this intention.

## C1 — Two deliveries of the same input

Question: should two accepted messages create two price changes?

Expected reasoning: transport receipt is not business identity. Locate the
effect-owning contract's stable operation identity and duplicate handling. Prove
the resulting business state and preserved history, not only the number of log
entries. A legitimate later correction must remain distinguishable from a retry.

Read [dependencies](../learning/04-UNITS-AND-DEPENDENCIES.md). A concrete identity
scheme is a realization decision, still not implemented in this example.

Required distinctions: delivery identity versus business-operation identity;
retry versus a legitimate correction; stored outcome versus log count.
Wrong answer: “Two messages always mean two price updates.”
Open contract: the owning unit's concrete identity and correction-version rules.

## C2 — Nothing arrives

Question: does silence mean prices are unchanged?

Expected reasoning: distinguish no expected work, missing expected input, a dead
observer and delayed evidence. Identify the agreed schedule and alert owner; do
not invent a supplier update. Check the observer's own last successful operation.
**[TARGET S07]** The September target specifies that Maestro remains idle when
there is no declared schedule.

**[EXPLANATION]** Read [evidence](../learning/06-EVIDENCE-RECOVERY-LEARNING.md).

Required distinctions: no work expected versus expected input absent;
supplier silence versus observer failure; schedule versus invented work.
Wrong answer: “No alert proves the import worked.”
Open contract: schedule, tolerance window, observer health and alert ownership.

## C3 — Permission is revoked while work waits

Question: does earlier acceptance guarantee execution is still authorized?

Expected reasoning: locate the revocation and execution-time authorization
contract; preserve a clear denied/cancelled outcome instead of bypassing current
authority. If the effect already happened, reconcile the actual state rather
than claiming a cancellation undid it.

Read [governance](../learning/01-INTENTION-AND-GOVERNANCE.md) and
[protection](../learning/03-CREATION-EXECUTION-PROTECTION.md).

Required distinctions: historical acceptance versus current authority;
cancellation before effect versus reconciliation after effect; denial versus bypass.
Wrong answer: “Once queued, a request stays authorized forever.”
Open contract: exact execution-time checks and revocation/commit race semantics.

## C4 — Effect committed, worker stops before acknowledgment

Question: can the queue safely retry?

Expected reasoning: distinguish Queue's lease from the consumer's effect. Inspect
durable effect identity, pending evidence and recovery rules. Reconcile before
repeating irreversible effects. Queue and Logger receipts alone cannot prove the
price change. Do not claim universal exactly-once execution from retries.

Read [dependencies](../learning/04-UNITS-AND-DEPENDENCIES.md) and
[recovery](../learning/06-EVIDENCE-RECOVERY-LEARNING.md).

Required distinctions: lease versus effect; acknowledgment versus effect proof;
reconciliation versus blind repetition after a missing acknowledgment.
Wrong answer: “Lease expiry proves no effect happened, so replay everything.”
Open contract: durable operation lookup, settlement and external-effect recovery.

## C5 — A newer agent replaces the implementation

Question: can it regenerate everything because its code is better?

Expected reasoning: separate reproducible code from irreplaceable state, preserve
historical quotations, qualify migration and restoration, compare old/new
behavior and obtain the appropriate rollout mandate. Improvement is established
by evidence; model novelty alone proves nothing.

Read [materialization](../learning/05-MATERIALIZATION.md).

Required distinctions: reproducible code versus irreplaceable data;
compatible interface versus compatible behavior; new capability versus permission.
Wrong answer: “A newer model may regenerate the database because its code is better.”
Open contract: migration, historical-data invariants and the authorized rollout gate.

## C6 — Another universe wants the supplier data

Question: is belonging to the same space enough?

Expected reasoning: identify the declared door, authorized caller, purpose,
permitted subset, retention and refusal behavior. Test the forbidden crossing
as well as the permitted one. A shared host or parent is not blanket consent.

Read [scopes](../learning/02-LAYERS-AND-SCOPES.md).

Required distinctions: shared containment/hosting versus data authority;
sender intent versus receiving authorization; permitted subset versus all data.
Wrong answer: “Same space means unrestricted cross-universe database access.”
Open contract: exact door-ratification roles (F-03b), schema and permitted retention.

## C7 — The log is green, but an old quote changed

Question: which evidence takes precedence over the success claim?

Expected reasoning: inspect the actual committed quotation and the source of its
change. A receipt establishes only its declared meaning. Preserve the discrepancy,
contain harm within the mandate, determine correction/repair/rebuild needs and
retest the observer that missed it. Do not rewrite evidence to match the claim.

Read [evidence](../learning/06-EVIDENCE-RECOVERY-LEARNING.md) and
[self-checks](../human/METACOGNITION.md).

Required distinctions: receipt integrity versus business correctness;
current evidence versus a desired success story; recovery versus evidence erasure.
Wrong answer: “Logger is green, so the changed accepted quote must be correct.”
Open contract: canonical quote invariants, evidence correlation and safe repair.

## C8 — A task was successfully repeated ten times

Question: is it now automatically a permanent mandate?

Expected reasoning: repetition can justify a proposal for automation, not its
authority. Identify the human-ratified standing mandate, limits, review, expiry
and STOP path before recurring action. Existing valid standing mandates do not
require redundant approval for every ordinary occurrence.

Read [governance](../learning/01-INTENTION-AND-GOVERNANCE.md).

Required distinctions: repetition versus ratification; standing scope versus
unbounded permission; a revoke path versus an obligation to run forever.
Wrong answer: “Ten successes automatically establish permanent authorization.”
Open contract: recorded standing-mandate conditions, review, expiry and revocation.

## Evaluating the answer

For each case, record the intention, governing source and status, authority,
state owner, affected relationships, observable success, failure response and
remaining unknowns. Medium agents use explicit steps. Strong agents also test
alternate implementations and cross-scope consequences. Humans explain the same
case at their chosen depth, without being required to recite infrastructure.

For a declared evaluation, a human evaluator or separate agent checks every
required distinction, rejects the listed tempting wrong answer, and asks for
transfer to a second situation. Record evaluator, snapshot, answers, outcome and
gaps in the external reading record. The author answering alone is a self-check,
not an independent qualification. A gap-only answer fails the teaching check.

Conceptual PASS requires all listed distinctions and honest unknowns; REVISE
means a distinction or transfer failed. Operational readiness is a separate
assessment and remains OPEN while governing contracts are missing. A conceptual
PASS therefore cannot be used as a deployment approval. See the
[worked answers](WORKED-ANSWERS.md) for the expected level of specificity.
