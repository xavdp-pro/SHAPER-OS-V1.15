# How to read and maintain this foundation

## Recipes are judged as recipes

The [7 October direction](../decisions/2026-10-07-INTENTIONAL-RECIPES.md)
separates the ideal scene and construction recipe from its concrete realization.
Assess intention, laws, functionality, boundaries and ordered dependencies here.
Do not attach "not implemented" to a recipe merely because it provides no code.
Implementation status and runtime tests belong to the realization's records.


Purpose: keep the ready-to-use V1.15 framework understandable, consistent and
easy to evolve. The editorial crosswalk is tracked in the
[ledger](../review/READING-LEDGER.md).

## One meaning, several ways to understand it

The [board](CONTEXT-INDEX.md) owns navigation. [Intent](../INTENT.md) owns the
repository boundary. Adopted decisions own changes of direction. Learning
chapters explain concepts; examples exercise them. The
[reconciliation ledger](../review/READING-LEDGER.md) owns completeness status.
Do not copy the same rule into several guides and let the copies evolve apart.

Agents read the full finite study set in the
[governing-corpus map](GOVERNING-CORPUS.md) before specializing. Human readers may
use their guide's subset and plain-language summaries; its prerequisites help
them when they choose greater depth. Human depth changes the amount of detail;
medium and strong agent routes change the reasoning support.
Neither changes permissions, evidence requirements or applicable law. Choose
the medium or strong route; both share the same local foundation.
No earlier edition or historical review is needed to begin.

## Four distinctions before relying on a document

- **Source:** what a participant actually said or a file actually contains.
- **Proposal:** an interpretation or design submitted for discussion and adoption.
- **Decision or governing requirement:** an explicit direction with scope and
  authority; a later date alone does not make it override another rule.
- **Evidence:** an observed result with conditions, date and limitations.

A source citation proves provenance, not truth. An example proves neither
deployment nor compliance. A well-written chapter does not close a missing-law
gap. Consult the [source map](../review/SOURCE-MAP.md) for these boundaries.

The root [LAW](../LAW.md) and [RULES](../RULES.md), and the local operational
contracts identified in the [governing corpus](GOVERNING-CORPUS.md), own their
stated obligations. Explanatory and decision material carries an explicit status
label at the sentence or owning section: **MANDATE** for direct operator direction, **EDITORIAL** for this
edition's reading/authoring procedure, **TARGET** for preserved scoped design,
**EXPLANATION** for teaching synthesis, and **OPEN** for unresolved questions.
A label applies from its position until the next heading or explicit label,
whichever comes first. After that boundary, the file's stated default status
applies unless a new label is present. It never silently carries a profile target
into a later generic section. Source IDs alone never confer authority.
Critical prescriptions cite the exact source section or operator passage.

An opening label expressly referring to the following chapter prose sets that
chapter's default status and sources; later explicit labels override it within
their bounded scope. After each such scope ends, the chapter default resumes.
An expressly explanatory illustration remains EXPLANATION even in a chapter
whose preserved vocabulary is TARGET; it never adopts a business policy.

## Chapter shape

Each learning chapter provides its prerequisites, status and source locators,
then answers: what is it, why does it exist, what happens in practice, what can
fail, and how can we verify understanding? Close with a next reading link.

Introduce the words before combining them. Increase difficulty in small steps.
Return to a concrete situation before adding another abstraction. Include a
counterexample or limit so a useful pattern does not become an absolute claim.

The five questions above are not the five human reading depths. Reader depths
are not organizational ranks, pilot qualification levels or crisis modes.

## Principal agent and context continuity

The principal agent needs the foundation explicitly defined by the
[governing-corpus map](GOVERNING-CORPUS.md), the relationship map and relevant
detailed contracts. A short task brief is not a substitute.
If context cannot hold everything at once, use staged reading with a durable
record and targeted rereads; never claim perfect retention or exhaustive reading
from a summary alone.

At each checkpoint record the revision or content digest, covered sections,
unread attachments, unresolved terms, sources of decisions and the next reading.
Before action, reload the exact governing requirements and affected contracts.
After a source changes, reread it and examine affected consumers rather than
assuming the old understanding remains valid.

Use the external record format, snapshot identity and replay procedure in
[verification and continuity](../review/VERIFICATION-AND-CONTINUITY.md).

## Complete reading through bounded outputs

**[EDITORIAL] Reading procedure:** tools can cap output by bytes or tokens even
when a requested line limit appears sufficient. The
[rulebook](../RULES.md#complete-rulebook) is split into seven smaller canonical
files so their complete bodies are easier to deliver and verify. This is a
structural reading aid, not a shorter law or a guarantee of retained context.

1. Identify the actual revision or dirty-state content manifest, the required
   documents and their canonical owners. Read the rule index's preamble and
   every one of its seven parts in order, plus the governing map's other
   required documents and applicable dependencies.
2. Inspect each delivered output for a truncation notice, missing tail or
   incomplete requested range. A search result, file name, requested limit,
   tool invocation or the agent's own assurance is not proof of full delivery.
3. If output is capped, resume at the next actually delivered line or section,
   using a smaller range. Repeat until the verified end of that file; then
   continue to the next canonical owner. Do not skip an unread middle range.
4. Record the file path, exact digest/revision, covered ranges and remaining
   gaps in the external reading record. Claim complete reading only when
   the recorded delivered ranges cover all required text at that checkpoint.
   Distinguish automatically supplied instructions from explicit file reads;
   if their completeness is uncertain, read the owning file explicitly.
5. After context compaction or session resumption, use that record to locate
   obligations and reload the exact rules and contracts affected by the next
   action. A coverage record proves delivery, not continuing understanding.

Keep ordinary rule files around 10–20 KB and below 25 KB where practical;
these are editorial size targets, not assumptions about any provider's limit.
Read in smaller ranges whenever the actual tool requires it. If a rule owner
grows, divide it at meaningful boundaries without dropping obligations,
duplicating their authoritative bodies or changing stable identifiers.

## Comprehension gate

Complete the [scenario checks](examples/COMPREHENSION-CHECKS.md). An acceptable
answer names the outcome, authority, state owner, dependency, failure behavior,
evidence and source. An unavailable contract is an explicit gap, not an invitation
to invent one. “Contract missing” alone cannot pass the teaching check: explain
the required conceptual distinctions as well. A human evaluator or separate
agent assesses a declared qualification attempt; solitary study is a self-check.
Use the exercises to develop understanding; track editorial crosswalk progress
separately in the ledger.

## Maintenance and change impact

For every substantive change, identify its owning document and update the board,
glossary, both agent routes, affected human explanations, examples and provenance
where necessary. Keep source archives unchanged. Record unresolved conflicts
instead of concealing them behind smoother prose. Check links and code-free
boundaries with tools kept outside this repository.
