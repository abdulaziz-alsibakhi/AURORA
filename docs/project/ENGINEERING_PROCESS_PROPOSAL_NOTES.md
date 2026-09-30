# Engineering Process — Proposal Notes

These are inputs for the proposal, not a second source of truth.

## Lifecycle choice

AURORA uses **lightweight Agile with milestone-driven Kanban and V-model-inspired verification/validation traceability**.

- **Waterfall:** too rigid for technical/research uncertainty.
- **Strict Scrum:** unnecessary roles and ceremonies.
- **Classical V-model:** too sequential.
- **Kanban + short milestones:** supports iterative execution and weekly review.
- **V-model traceability:** connects requirements to verification, validation, evidence, and claims.

## Engineering practices to reflect in the proposal

Where appropriate, document:

- short milestones decomposed into weekly outcomes;
- measurable functional/non-functional requirements;
- alternatives and rationale for major design choices;
- Git configuration/change management;
- protected `main`, short-lived branches, PRs, and peer review;
- CI and automated testing;
- unit/component/integration/system verification as applicable;
- verification versus domain/scientific validation;
- requirement → implementation → test/experiment → evidence traceability;
- reproducible experiments and identifiable baselines;
- live risks and mitigations;
- failure/robustness testing;
- primary + backup/reviewer ownership;
- individual contribution evidence.

CI proves only that defined automated checks passed. It does not establish reservoir-physics or scientific validity.

OPM Flow is a higher-fidelity numerical reference, not physical ground truth.

Integrate these ideas into the existing proposal sections on requirements, architecture, alternatives, validation, experiments, feasibility, risks, project management, schedule, engineering relevance, and limitations.

Do not attribute team-selected practices to the professors unless an explicit source supports that attribution.
