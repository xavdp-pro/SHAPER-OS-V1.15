# Worked answers at two reading depths

Status: EXPLANATION; fictional teaching examples, not executed tests, adopted
business policy or a claim that the missing operational contracts exist.
Prerequisites: [C4 and its rubric](COMPREHENSION-CHECKS.md),
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
6. **Open contract.** This candidate does not yet supply operation-identity lookup,
   safe settlement and revocation-race contracts. Those are F-05 gaps. The
   conceptual response is valid, but operational recovery is not authorized by
   this answer alone and cannot be certified from it.

This answer meets the conceptual rubric by distinguishing lease from effect,
acknowledgment from proof, and reconciliation from blind replay. A real evaluator
still asks the learner to explain another case; reading this model answer does
not itself demonstrate independent understanding.

## Transfer question

A document upload was stored, but the client did not receive confirmation.
Explain which distinctions remain the same and which new contracts are needed
for document identity, versions and duplicate imports. Do not simply replace
“price” with “document”: two uploads may intentionally create separate versions.
