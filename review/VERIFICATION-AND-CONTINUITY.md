# Revision evidence and reading continuity

Status: editorial procedure for this candidate; no runtime qualification.

## Snapshot identity before Git publication

Until the candidate has a committed revision, identify a checkpoint by a sorted
manifest of every relative file path and its SHA-256 content digest. Store the
manifest outside SHAPER OS to avoid self-hashing recursion. Name the checkpoint
and hash the manifest itself; retain the exact bytes used. A date alone is not a
revision, and a previously correct summary is not evidence of unchanged files.

For each checkpoint, the operator evidence record names the document root, file
count, manifest location/digest, checker location/digest, command used, exit
status and output. Keep machine-specific locations in that external evidence
record rather than making them generic laws.

## Reading record location and minimum fields

Keep a private `reading-records/<checkpoint>/<actor>.md` under the operator's
task evidence workspace, not inside the generic foundation. Record:

- actor and role, checkpoint manifest and date;
- selected reading route and rationale, distinct from authority or model access;
- each source path, exact revision or digest and covered sections;
- read in full, partial, absent or not read; never replace this with “indexed”;
- understood relationships and scenario answers with source/status;
- unresolved contradictions, missing attachments and affected obligations;
- current task mandate, operational governing revision if applicable;
- next reading/action and the documents to reload before it.

On resumption, compare the source manifest with current files. Reread changed
files and their affected consumers, as well as governing text not reliably
available. An unchanged digest proves content identity, not retained understanding.
Transfer the record when moving workspaces; an unavailable record means coverage
must be re-established rather than silently assumed.

## External checker and replay

Checker identity: **SHAPER-READING-CHECKER-v2**. The current operator evidence
record, attached to the task that produced this checkpoint, carries the exact
script path and content digest. Preserve it with the manifest and output.

The checker checks local Markdown links, README reachability, document-only
files, chapter prerequisites and pedagogy, provenance labels, profile/corpus
navigation and scenario rubric coverage. It never fetches external content,
reads secrets or mutates the candidate. A different machine may place it elsewhere;
verify its recorded digest and supply the candidate root as its argument.

If the referenced checker cannot be retrieved, mark its replay unavailable.
A new checker may be written **outside** SHAPER OS against these declared checks,
but it receives its own digest and run record. Do not claim the older run was
reproduced without its inputs and implementation.

## Release and evaluation

Before publishing a V1.15 release, establish a Git commit/tag identity, archive
the bounded source and reading manifests, finish the rule crosswalk and open
contracts, rerun structural checks, and record independent scenario evaluation.
A human study session or self-check can happen now; it does not certify full
operational readiness. No teaching score substitutes for deployed proof.
