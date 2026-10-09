# Example: a document universe expressed as an intentional recipe

## Illustrative Example (Non-Binding / Demonstration Only)

This example shows how an agent derives a coherent composition from intentions
and laws. It does not prescribe a document product for every SHAPER universe.
Specialized analysis algorithms and engine choices belong in the owning recipe.
See the [recipe direction](../../decisions/2026-10-07-INTENTIONAL-RECIPES.md).

**Ideal scene:** a person deposits a document, can retrieve its original, and
can ask questions whose answers identify the exact permitted source version.

- A document hub preserves originals, versions, ownership and access.
- A separate analysis function extracts and interprets content, preserving
  uncertainty and provenance; the hub does not perform that analysis.
- A semantic retrieval function splits the approved content into meaningful
  chunks, obtains embeddings and maintains a derived searchable index.
- These functions can share one document-universe maintenance perimeter while
  retaining separate responsibilities and private state.
- A control cockpit calls their authorized interfaces; it does not absorb their
  storage, analysis or vector engine into its own maintenance perimeter.

**Construction order:** define ownership and permissions; preserve originals;
connect analysis; define chunking and embedding; build retrieval; exercise the
whole intended journey and its revocation/recovery behavior in the realization.
The recipe explains what to build. Its implementation and test record are separate.
