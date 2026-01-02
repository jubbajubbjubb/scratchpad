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


## WHY THE CURRENT SPEC IS INCORRECT


## DESIGN GOALS


## CONSTRAINTS & NON-GOALS


## OPEN QUESTIONS
