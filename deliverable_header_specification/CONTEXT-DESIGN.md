# CONTEXT — DELIVERABLE HEADER ONTOLOGY

## TRIGGER

This design pass was triggered during evaluation of a structural invariant
governing artifact organization: one artifact per path, with exactly one
associated header.

While validating this invariant against existing specifications, an
implicit assumption surfaced in the Deliverable Header specification:
that deliverable headers are embedded within artifact bodies.

This assumption became visible while reasoning about directory-scoped
artifacts, fixed header filenames, and the requirement that artifact
bodies remain opaque to tooling and orchestration.

At that point, it became clear that the Deliverable Header specification
describes an embedded-header model that is incompatible with the
emerging artifact ontology, necessitating a scoped design review.


## PREVIOUS ASSUMPTION (NOW INVALID)

The Deliverable Header specification implicitly assumed an embedded-header
model.

Under this assumption, a deliverable artifact was treated as a single
file containing both header and body content, with the header appearing
as a structured block at the beginning of the artifact.

Header/body separation was established textually through explicit
delimiters, and discovery of header information required parsing the
artifact content itself.

This model further implied that:
- deliverable artifacts are file-scoped rather than directory-scoped,
- header presence is enforced through content structure rather than
  placement,
- and artifact bodies are expected to be inspected to access metadata.

This assumption was not explicitly declared, but was reflected throughout
the specification language and examples.


## NEWLY EXPLICIT TRUTH

A deliverable artifact is a directory-scoped unit, not a single file.

Each deliverable artifact is associated with exactly one deliverable
header, which exists as a standalone file named `HEADER.txt`.

The deliverable header is not embedded within the artifact body.
Artifacts themselves do not contain headers.

Association between a deliverable header and its corresponding artifact
is established solely through directory co-location.

The presence, uniqueness, and association of the deliverable header are
structural properties of the artifact directory, not properties of the
artifact body.

As a result, artifact identity, header structure, and artifact content
exist in separate namespaces and must not be conflated.

Any specification language that treats headers as embedded content, or
that derives header presence from artifact body structure, is
incompatible with this model.


## WHY THE CURRENT SPEC IS INCORRECT

The current Deliverable Header specification encodes an embedded-header
model that is incompatible with the newly explicit artifact ontology.

Specifically, the specification assumes that:
- the deliverable header is a block of text embedded within the artifact
  body,
- header and body are separated by textual delimiters,
- and header presence, structure, and association are properties of the
  artifact content itself.

Under the clarified model, these assumptions are false.

Deliverable artifacts are directory-scoped units, and deliverable headers
exist as standalone files colocated with, but not contained within, the
artifact body. As a result, header presence and association are enforced
structurally by placement rather than by content.

Because the current specification defines header structure, boundaries,
and placement in terms of embedded content, it cannot correctly describe
or govern a system in which:
- artifacts do not contain headers,
- header discovery must not require parsing artifact bodies,
- and a fixed header filename is used.

This mismatch is ontological rather than stylistic. The specification is
internally consistent under its original assumptions, but those
assumptions no longer hold.

Any continued use of the embedded-header language risks reintroducing
implicit parsing requirements, filename collisions, and ambiguous
interpretation when applied to a directory-scoped artifact model.


## DESIGN GOALS

Clarify the ontology of deliverable headers so that the specification
correctly describes a directory-scoped artifact model.

Ensure the Deliverable Header specification explicitly reflects that:
- deliverable artifacts do not contain headers,
- deliverable headers exist as standalone structural files,
- and header association is established through directory co-location.

Eliminate embedded-header language that implies artifact body parsing,
textual header boundaries, or file-scoped artifacts.

Preserve the existing semantic intent of header fields, including their
role as declarative fact surfaces that do not encode authority,
lifecycle, ordering, or evaluation.

Enable deterministic, non-inferential discovery of deliverable headers
by tooling and orchestration without inspecting artifact body content.

Maintain compatibility with artifact-first governance principles,
including explicit declaration, mechanical determinism, and loud failure
on ambiguity.

Limit changes strictly to the Deliverable Header specification, avoiding
unnecessary impact to naming grammar, invariants, protocols, or
enforcement mechanisms.


## CONSTRAINTS & NON-GOALS

This design effort is constrained to modifying the Deliverable Header
specification only.

The following constraints apply:

- The modification MUST preserve the existing header field set and their
  semantic intent as declarative fact surfaces.
- No header field may be repurposed to encode authority, lifecycle,
  ordering, evaluation, or acceptance.
- The corrected specification MUST remain compatible with explicit,
  non-inferential, mechanically enforceable governance principles.
- The design MUST assume exactly one deliverable header per artifact,
  named `HEADER.txt`, associated by directory co-location.
- The design MUST NOT require parsing or inspecting artifact body content
  to discover header information.

The following are explicit non-goals of this design pass:

- Defining or modifying naming grammar beyond what is strictly necessary
  to describe header structure and association.
- Defining artifact body file naming rules or constraining artifact body
  structure.
- Introducing enforcement mechanisms, tooling behavior, or orchestration
  logic.
- Resolving legacy migration strategy beyond acknowledging historical
  embedded-header artifacts.
- Modifying invariants, protocols, placement specifications outside the
  Deliverable Header spec, or repository topology.
- Optimizing for convenience, ergonomics, or backward compatibility at
  the expense of structural clarity.

Any requirement that cannot be expressed within these constraints is out
of scope and must be addressed through a separate design pass.


## ADDITIONAL FINDINGS

The following findings were surfaced during this design pass and are
recorded here as explicit facts. All items listed below are resolved and
do not represent open questions or pending decisions.

### Global Structural Header Filename

Deliverable headers use a fixed structural filename: `HEADER.txt`.

`HEADER.txt` is a global structural filename with fixed meaning. It is not
an artifact body, is not governed by `ARTIFACT_ID`, and is not subject to
naming grammar or placement derivation.

Its presence is structural and universally recognized by tooling and
orchestration without inference.

### Artifact Identity Collision Prevention

An artifact whose `ARTIFACT_ID` resolves to `HEADER` is structurally
incompatible with the directory-scoped artifact model.

Because `HEADER.txt` is required to exist within every artifact
directory, allowing an artifact named `HEADER` would create an
unavoidable filesystem collision.

To preserve mechanical determinism and filesystem validity, the token
`HEADER` is treated as a structurally reserved token and is forbidden for
use as an `ARTIFACT_ID`.

This reservation is structural rather than semantic and is escalated to
governance for formal declaration via a **STRUCTURAL RESERVED TOKENS**
policy.

### Header Scope and Discovery Model

Deliverable artifacts are directory-scoped units.

Each deliverable artifact directory contains exactly one deliverable
header file named `HEADER.txt`.

Deliverable headers are standalone plaintext artifacts and are not
embedded within artifact body content.

Header discovery is performed exclusively via deterministic filename
lookup. Tooling and orchestration MUST NOT inspect, parse, or infer header
information from artifact body content.

Failure to locate exactly one valid `HEADER.txt` within an artifact
directory constitutes a structural failure and MUST result in loud
failure.

### Structural Filename Governance

Structural filenames (such as `HEADER.txt`) are treated as a finite and
explicitly governed set.

The Deliverable Header specification does not enumerate or reserve
structural filenames beyond `HEADER.txt`.

Any expansion of the structural filename set is out of scope for this
design pass and must be introduced through explicit governance policy
updates.
