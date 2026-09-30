# Supervisor Feedback Register

## Purpose

This document converts actionable supervisor feedback into durable project inputs.

It is not a transcript and does not reproduce private meeting material. Raw meeting
records remain separate from the public engineering specification.

The register records the engineering consequence of feedback so that important
concerns do not disappear into chat history.

## Current feedback themes

### Domain credibility and result interpretation

**Concern**

The team must be able to judge whether reservoir-related outputs and assumptions are
meaningful. A dataset manual alone is not sufficient domain validation, and routine
operation cannot depend on asking an external expert to approve every simulation.

**Project response**

- build a bounded reservoir-domain knowledge base;
- define variables, units, assumptions, and constraints explicitly;
- ground domain-sensitive claims in authoritative sources;
- define validation rules before relying on results;
- seek bounded qualified review for important assumptions and interpretation;
- distinguish simulator consistency from real-field validation.

**Roadmap impact:** Phases 1, 2, 4, 10.

### Engineering-program relevance

**Concern**

The team must be able to explain how AURORA is a Software/Computer Engineering
project despite using reservoir engineering as its application domain.

**Project response**

The engineering contribution is framed around software architecture, simulator
integration, ML/RL, optimization software, model-mismatch handling, data/provenance,
verification, robustness, reproducibility, telemetry, and human interpretation.

Reservoir engineering supplies domain context and constraints; the team does not claim
to replace reservoir-engineering judgment.

**Roadmap impact:** Phases 1–3 and all formal deliverables.

### Shared understanding and bus factor

**Concern**

Important project knowledge must not exist only with one team member.

**Project response**

- primary ownership without exclusivity;
- backup/reviewer assignments;
- canonical subsystem documentation;
- interface contracts;
- reproducible procedures;
- review through pull requests;
- each member understands the complete loop and adjacent interfaces.

**Roadmap impact:** Phase 0 and every subsystem phase.

### Alternative designs and justification

**Concern**

The project must show engineering design reasoning rather than merely naming tools
or algorithms.

**Project response**

Consequential design choices should identify alternatives, criteria, trade-offs, and
rationale. Important decisions are preserved through ADRs and reflected in the
proposal/final report.

**Roadmap impact:** Phases 2, 3, 6, 7, 9.

### Presentable demonstration

**Concern**

A second reader should not be expected to interpret unexplained terminal output or
raw numerical dumps.

**Project response**

The project includes a dedicated human-interpretation/demo phase and requires
presentation-ready views of reservoir state, controller behaviour, safety
interventions, model mismatch, evidence, and failure behaviour.

**Roadmap impact:** Phase 11, with enabling telemetry beginning earlier.

### Quantitative evidence

**Concern**

Claims of usefulness or correctness require understandable numerical evidence.

**Project response**

Requirements define measurable success criteria; experiments preserve provenance;
the final evaluation compares explicit baselines and metrics; figures/numbers remain
traceable to reproducible runs.

**Roadmap impact:** Phases 2, 9, 10.

### Individual contribution

**Concern**

Capstone assessment includes individual contribution. Each member should own and be
able to explain meaningful work.

**Project response**

Ownership, issues, pull requests, reviews, experiment evidence, and deliverable
contributions provide a durable contribution record. Contribution is not reduced to
commit count.

**Roadmap impact:** all phases.

### Hardware scope

**Status: PARKED / UNRESOLVED**

Supervisor feedback questioned whether a hardware component was sufficiently
integrated with the core project.

The team is deliberately not resolving this item in the current baseline because
Timur intends to discuss it with the professor. No core architecture or ownership
dependency should assume hardware is included or excluded until that discussion is
reconciled and recorded.

## Using this register

Feedback becomes actionable through the requirements traceability system.

A concern is not considered addressed because this document says "we will handle it."
It is addressed only when the linked requirement, implementation/documentation, and
evidence satisfy their acceptance criteria.
