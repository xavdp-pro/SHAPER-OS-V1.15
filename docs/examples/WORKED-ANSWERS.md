# Worked answers at two reading depths

Purpose: **EXPLANATION** through fictional worked examples at two reading depths.
Use them to connect the concepts to practical reasoning; the chosen realization
supplies its business policy, operating contracts and execution evidence.
Prerequisites: [C4, C9 and their rubrics](COMPREHENSION-CHECKS.md),
[governance](../learning/01-INTENTION-AND-GOVERNANCE.md) and
[dependencies](../learning/04-UNITS-AND-DEPENDENCIES.md).

## C4 at human Level 2

The import stopped after it may have changed prices, but before saying it was
finished. I cannot conclude “nothing happened” from the missing reply. Repeating
the whole request immediately might apply a change twice or send duplicate notices.

I want the responsible operator to check which supplier update this was, whether
the prices were actually saved and whether old accepted quotes stayed unchanged.
The queue's acknowledgment would tell me about work handling, not prove those
business facts. Before any repeat, we must know the unit's recovery rule and
whether the original permission still applies. If those facts cannot be checked,
the honest status is unresolved, not successful or automatically safe to retry.

Evidence I would ask to see: the actual resulting price, one preserved accepted
quote and the operation's recorded status. I would not ask the operator to expose
passwords or all customer records to explain this single case.

## C4 at medium-agent depth

1. **Intention and authority.** Preserve the agreed effective price and old quote
   commitments. The missing acknowledgment creates no expanded mandate. Identify
   the existing realization's governing revision and current authority before
   performing any operational recovery.
2. **Known facts and uncertainty.** The scenario states a committed effect followed
   by a worker stop. Queue settlement may still be absent. In a real incident,
   verify that statement from the effect-owning unit rather than inferring it
   merely from a log or timeout.
3. **Ownership.** Queue owns deferred-work responsibility and its lease; the
   consumer owns the price effect; Logger owns its authenticated evidence receipt.
   None of those receipts alone substitutes for inspecting the business state.
4. **Recovery decision.** Look up the stable operation identity and persisted
   effect according to the consumer contract. Reconcile the completed effect and
   pending evidence/settlement before considering a retry. Lease expiry does not
   prove absence of an effect. Do not promise universal exactly-once behavior.
5. **Proof.** Compare the actual price/effective date with the authorized input,
   confirm an earlier accepted quote is unchanged, and correlate effect and
   work/evidence records. If a notification is a required external effect,
   reconcile its delivery separately rather than blindly sending it again.
6. **Realization contract.** Locate operation-identity lookup, safe settlement
   and revocation-race behavior in the chosen realization, applying the local
   [Queue contract](../contracts/queue.md) and [lifecycle](../agent/LIFECYCLE.md).
   Use the actual contract and recovery mandate
   to turn this conceptual response into an operational action.

This answer meets the conceptual rubric by distinguishing lease from effect,
acknowledgment from proof, and reconciliation from blind replay. A real evaluator
still asks the learner to explain another case; reading this model answer does
not itself demonstrate independent understanding.

## C9 at human Level 2

Last month's failed import remains a fact. It does not tell me whether today's
corrected input will fail. I would ask the responsible operator to show that the
mapping is valid now and that the requested preview is permitted. If so, a
bounded preview can show the proposed prices without changing accepted quotes.
It is not permission to publish those prices. If the mapping is still invalid
or permission was withdrawn, stopping remains appropriate. The lesson should say
when it applies, rather than “never import prices again.”

## C9 at medium-agent depth

1. **Separate event and lesson.** Keep the permitted record of the earlier failed
   mapping and its source. Treat the blanket ban as an interpretation, not law.
2. **Inspect current prerequisites.** Verify the corrected mapping against this
   input and locate the current mandate. A remembered fix is not fresh validation.
3. **Keep ownership and scope.** The price-owning unit owns validation and effects;
   a lesson or reviewer cannot grant live-update authority. Inspect the preview
   contract in the chosen realization before using its preview capability.
4. **Choose a proportionate response.** With verified prerequisites and preview
   authority, attempt the bounded preview. With an invalid mapping or revoked
   permission, use the declared refusal/alternative and report the reason.
5. **Compare outcomes.** Inspect proposed prices and preserved accepted quotes;
   check that no live effect occurred. Compare the contrasting invalid-input case.
   A successful preview does not prove a successful production import.
6. **Revise only the supported lesson.** Qualify the lesson by mapping version,
   validation and mandate conditions; retain the earlier observation under the
   applicable retention rules. If these contracts or observations are absent,
   state the gap instead of executing from this model answer.

## C10–C12: concise worked responses

**C10 — Purpose before completion.** My mandate covers new quotations, not
rewriting accepted ones. The consumer's accepted-quote invariant takes precedence
over the completion metric; reviewer support grants no exception. I would use
the allowed update path, or ask the exception owner if none exists. Without the
effective date I would not publish a guessed date; independent authorized work
can continue. Proof needs both the new price and an unchanged accepted quote.
Locate the update/exception contracts in the chosen realization. Transfer: a faster
document import must not overwrite a retained signed version to improve its count.

**C11 — Useful waiting versus repetition.** This latest identical probe tells me
nothing new. First I check whether waiting is expected under the schedule and
whether the declared deadline still allows it. Otherwise I choose a permitted
new observation or hand off the unresolved input to the schedule/alert owner with
the supplier's validated delivery as the resumption trigger. I would recheck
permission and any uncertain prior effect when it arrives. The actual deadline,
retry budget and responsible owner need the realization's contract; they cannot
be guessed here. Transfer: an expected document upload delay differs from endlessly
retrying an upload that may already have been stored.

**C12 — Verify the corrector.** The consumer shows the expected price operation
already committed, while the observer requests replay. I would correlate those
records before calling either one wrong. With a verified false alert, I would
contain further replay only through an authorized control and route structural
repair to the external owner, keeping the discrepancy visible. New evidence can
revise my diagnosis, not authorize a bypass. Retesting must also include a truly
missing import, or suppressing false alerts could hide genuine failures. Correlation,
containment and repair contracts remain open. Transfer: check a document indexer's
alert against the stored version before reimporting or discarding all alerts.

## Transfer questions

A document upload was stored, but the client did not receive confirmation.
Explain which distinctions remain the same and which new contracts are needed
for document identity, versions and duplicate imports. Do not simply replace
“price” with “document”: two uploads may intentionally create separate versions.

For C9, an earlier document import failed on an unsupported encoding. A new
decoder is available. Explain what must be checked before a permitted preview,
how original documents remain preserved, and why decoder availability alone
neither proves validity nor authorizes replacing stored versions.
