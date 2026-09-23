# 6. Evidence, recovery and learning

Status: explanatory synthesis; no installed qualification is claimed.
Prerequisite: [materialization](05-MATERIALIZATION.md).
Sources: S03, S04, S06 and S07 in the [source map](../../review/SOURCE-MAP.md).

## In plain language

A green status or an acknowledgment does not prove the promised result happened.
Check the real effect and practise recovery. Also check that the mechanisms
watching for failures can notice their own failures.

**[EXPLANATION S03: OS master sections 8 and 14–21; Runtime master sections 12,
19–20 and 27]** This chapter teaches evidence and recovery distinctions, not a
claim of qualified runtime behavior.

## What is it?

Evidence connects a claim to an observable effect and its conditions. Distinguish
sent, received, understood, accepted, executed and verified. Availability,
health, integrity and trustworthiness are also distinct: a compromised service
can still answer requests.

Recovery restores the intended capability with its state and trust boundaries.
Learning compares expected and observed effects, then revises interpretations or
proposes changes to governing rules through the proper authority.

## Why does it exist?

Without these distinctions a green status page can conceal a failed business
result, and a successful backup command can conceal an unusable recovery point.
The correction mechanism itself may also be broken or blind.

## In practice

For a price update, inspect the actual stored price and a newly calculated quote,
confirm an earlier accepted quote is unchanged, and correlate the operation's
evidence. If notification is required, verify that specific outcome separately.
Prove restoration with a controlled recovery exercise rather than only checking
that an archive exists. Unit restoration and coherent universe restoration are
different scopes and need compatible recovery points and dependency handling.

## What can fail?

One sensor certifies itself; evidence is missing but success is declared; a
restored unit replays an external effect twice; or local recovery damages another
universe. Preserve evidence, contain the fault and name the required intervention:

**[EXPLANATION S03: OS master section 15]** The four intervention names mean:

- CORRECT changes a known faulty rule, configuration or implementation.
- REPAIR restores valuable state that cannot simply be regenerated.
- REBUILD recreates a reproducible component from trusted sources.
- QUARANTINE isolates a suspect participant while preserving evidence.

These are not the same axis as development, testing and production environments.
The cause of compromise must be addressed before trusting a rebuilt component.

## How do we verify understanding?

Name the evidence for the result, the evidence for recovery, the observer's own
health and a condition that would invalidate the conclusion. Do not call a
self-review independent by giving it a second role name. Review from governance,
human/organization and failure/recovery perspectives; record a genuinely
independent counter-view when one was obtained and its absence when not.

Next: [different human and agent self-checks](../human/METACOGNITION.md), then
[the scenario exercises](../examples/COMPREHENSION-CHECKS.md).
