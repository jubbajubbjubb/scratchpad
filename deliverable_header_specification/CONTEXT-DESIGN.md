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


## DESIGN GOALS


## CONSTRAINTS & NON-GOALS


## OPEN QUESTIONS
