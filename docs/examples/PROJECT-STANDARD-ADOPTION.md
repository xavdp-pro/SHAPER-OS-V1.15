# Adopting SHAPER OS in an existing project

This example records an explicit human adoption under
[LAW's adoption and scope contract](../../LAW.md#two-uses-and-explicit-adoption).
It is a project entrance, not a replacement for the
[full reading required by AGENTS](../../AGENTS.md). A human instruction establishes
the adoption; writing the record does not require a second approval.

## Prompt: align an ongoing project

Use this prompt when the human wants an existing project to adopt SHAPER OS
as its development standard. It starts from the project's actual architecture,
working paths and current mandate; it does not request a new universe or a
wholesale rewrite. The prompt selects a published revision when it is used,
then pins that revision for an inspectable assessment. No particular commit,
model provider, agent tool or project technology is assumed.

```text
Adopt SHAPER OS V1.15 as the governing development standard for this project,
within the current human–agent mandate.

Repository:
https://github.com/xavdp-pro/SHAPER-OS-V1.15

Use the immutable revision explicitly selected by the human when one is supplied.
Otherwise, resolve the repository's published default branch once at the start
of adoption. Record the full commit SHA and verify that the corpus you read
matches that exact revision. Use that pinned revision throughout the adoption
assessment. Do not silently switch revisions during the work.

Follow its AGENTS.md, LAW.md, governing map and reading contract. Complete the
required reading and applicable contract dependencies before making changes.

Treat applicable SHAPER OS obligations as binding requirements, not optional
background context. This adoption covers ongoing development; it does not
require rebuilding the project or creating a new universe.

Identify the project's actual architectural roles, components and applicable
profiles. A component already declared as a SHAPER universe or functional unit
retains all its applicable obligations.

Preserve existing implementations, data, configuration and verified working
paths. Reuse valid evidence where the implementation and conditions remain
unchanged.

Report:
1. Your understanding of SHAPER OS and its application to this project.
2. Obligations already satisfied, with inspectable evidence.
3. Confirmed conformity gaps, their consequences and affected components.
4. A proportionate correction plan within the current mandate.

Distinguish an unverified condition from an observed defect. A documented gap
does not waive an applicable obligation. Do not introduce an unrelated
migration or wholesale rewrite.

Record the repository URL, adopted full commit SHA and project scope in the
project's agent instructions. If adoption is already recorded, compare the old
and selected revisions, assess the changed obligations and their impact, then
record the deliberate pin update and any gaps within this adoption mandate.
The human's instruction to adopt the selected revision can itself authorize
that update; do not request a second approval for the same decision. Preserve
the existing scope unless the human mandate changes it, and resolve any
genuinely uncovered conflict before its dependent action. Later upstream
changes alone do not advance the project's recorded pin.

Continue ordinary authorized development without requesting approvals already
covered by the mandate. Resolve genuinely missing decisions before their
dependent actions.

Keep implementation, tests, deployment, live operation and human acceptance
clearly distinguished.

Communicate with me in French; write technical artifacts in English.
```

## Record the adoption in project instructions

Place the following section in the project's agent instructions. Replace every
placeholder with actual facts and accessible references; do not infer an adoption,
a conformity claim or an exception from this template. The corpus stays code-free;
the existing project keeps its implementation and operating records.

```markdown
## Adopted development standard

The human–agent tandem has explicitly adopted SHAPER OS as the governing
development standard for this project's declared scope. Treat its applicable
obligations as binding requirements, not optional background context.

- Corpus location: <accessible corpus path>
- Immutable revision: <full commit SHA or content-manifest digest>
- Adoption scope: <project components and development responsibilities>
- Declared architectural roles and applicable profiles: <actual declarations>
- Existing conformity gaps: <rule/contract, observed gap, consequence,
  authorized correction scope and required evidence>
- Work outside the current mandate: <actual exclusions>

Follow the corpus's AGENTS.md, LAW.md, governing map and reading contract.
Read the required foundation and applicable detailed contracts before work.

Continue ordinary development covered by the current mandate. Preserve
existing state and unaffected contracts. Apply construction or migration
procedures only when the authorized task requires them.

A declared gap does not waive an applicable obligation. Do not claim full
universe or unit conformity from adoption of the development standard alone.
Report the actual scope, changes, evidence and remaining gaps.
```

Non-applicability is justified by a contract's subject and conditions, not by the
cost of meeting it. An existing declared SHAPER unit or universe keeps its
applicable profile obligations. Record uncertainty as uncertainty, not as a
self-granted exemption, and resolve it before the dependent action while
continuing independent work already authorized.
