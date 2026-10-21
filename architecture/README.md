# Architecture specification — Sarah

Generated from Ergane. This bundle is the architecture of this system as
a **knowledge graph**: the canvas definitions are the class layer, the
entities are typed instances, and the edges are the traceability.

## Read in this order

1. **The architecture description documents** — one markdown file per
   Ergane document, named for the document, beside this README. Prose
   first: they say what this system is for and how it hangs together.
   - [`architecture/objectives-and-business-case.md`](objectives-and-business-case.md)
   - [`architecture/architecture-description.md`](architecture-description.md)
   - [`architecture/requirements-specification.md`](requirements-specification.md)
   - [`architecture/decision-log.md`](decision-log.md)
2. **`graph.json`** — the backbone. `nodeTypes` (what kinds of things
   exist), `nodes` (every artifact, with the path to its data and when
   it was last changed), `edges` (typed relationships: requirement →
   decision → model shape → capability).
3. **`entities/<type>/INDEX.md`** — one line per artifact of a type. Use
   these to navigate; read individual `.codl.json` files only as needed.
4. **`definitions/<typeIri>.codl-def.json`** — what a type's fields MEAN,
   their legal values, and which other types it may link to. Authored by
   the professional body (IASA BTABoK); **read-only**.
5. **`models/`** — the architecture models: `*.calm.json` in FINOS CALM,
   `*.model.json` in another notation, each with a `*.links.json` overlay
   mapping model elements to the decisions and requirements that govern
   them. An interface model is projected to CALM too, with the whole
   contract under `io.btabok.interface`.

The documents annotate the graph; where they disagree with it, the graph
is the record.

## Contents

33 entities · 19 types · 2 models · 4 documents · 6 edges

## Rules for agents working in this repository

- Treat this bundle as **specification**: when code and spec disagree,
  that is a finding to report, not a licence to change the spec.
- `definitions/` is **read-only**. It comes from the BTABoK library.
- Do not hand-edit anything under `architecture/` — this README and the
  documents beside it included. It is all regenerated on every publish
  and your edit is lost. Propose changes as change-sets against Ergane
  (see `CHANGES.md`).
- Ergane owns `architecture/` plus exactly the paths listed under
  `ownership.machineOwnedPaths` in `manifest.json`. Everything else in
  this repository is yours and is never touched by a publish.
- Layout/board information is deliberately excluded: position is not meaning.
