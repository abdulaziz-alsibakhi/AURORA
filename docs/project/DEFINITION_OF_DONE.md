# Definition of Done

## Purpose

AURORA does not define completion as "someone wrote code."

Completion means the work has reached the level of implementation, verification,
documentation, evidence, and integration appropriate to its type.

## Universal Definition of Done

A meaningful work item is Done when, where applicable:

- its acceptance criteria are satisfied;
- implementation or documentation is present in the canonical repository;
- relevant tests/checks pass;
- important assumptions are explicit;
- relevant documentation is updated;
- evidence required by the issue is preserved;
- dependent interfaces have not been silently broken;
- the work has received appropriate review;
- unresolved limitations are recorded rather than hidden;
- the pull request is merged to `main`; and
- the corresponding GitHub issue reflects the final outcome.

Not every bullet applies equally to every issue. The issue should make the applicable
completion evidence clear.

## Engineering work

Engineering work normally requires:

- implementation;
- verification;
- integration compatibility;
- relevant documentation; and
- review.

A feature that works only on the author's machine is not Done.

## Scientific or experimental work

Scientific/experimental work additionally requires:

- explicit experiment purpose or hypothesis;
- identifiable data/configuration;
- reproducible execution where feasible;
- preserved metrics/results;
- interpretation tied to the defined metric;
- negative or failed outcomes retained when informative; and
- claims no stronger than the evidence supports.

**Code without evidence is not a completed scientific milestone. Evidence without
reproducible code/configuration is not a completed engineering milestone.**

## Documentation work

Documentation is Done when:

- it has a clear canonical purpose;
- it does not create a competing source of truth;
- claims are sourced where required;
- unresolved facts are labelled unresolved;
- links and references resolve; and
- the document is understandable to its intended reader.

## Milestones

A milestone is not complete because its target date passed.

It is complete when all mandatory milestone outcomes satisfy their acceptance gates,
or when an approved scope/change decision explicitly redefines the gate.

## Roadmap phases

A roadmap phase is complete only when the exit gate in `ROADMAP.md` is satisfied.

Issues may continue beyond a phase for non-blocking improvements, but unresolved
requirements that invalidate the exit gate prevent the phase from being called
complete.
