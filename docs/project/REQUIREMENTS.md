# AURORA Project Requirements

## Purpose

This document defines project-level requirements that can be stated responsibly at
the current maturity level.

Detailed technical requirements are refined during ROADMAP Phase 2. Unknown
domain-sensitive values, interfaces, and thresholds must not be invented here.

Requirement identifiers provide stable traceability across issues, evidence, and
formal deliverables.

## Requirement status

- **Active** — currently required.
- **Provisional** — required in principle but details remain to be frozen.
- **Unresolved** — a project decision is still pending.
- **Superseded** — retained for history but replaced by a later requirement/decision.

## Project and course requirements

### AUR-REQ-001 — Clear project objectives

**Status:** Active

AURORA shall define clear project objectives and measurable criteria for evaluating
progress toward them.

### AUR-REQ-002 — Functional and non-functional requirements

**Status:** Active

AURORA shall maintain measurable functional and non-functional requirements
appropriate to the current project maturity.

### AUR-REQ-003 — Engineering-program relevance

**Status:** Active

The project shall explicitly identify the Software/Computer Engineering knowledge,
methods, and design work contributed by each relevant subsystem and team member.

### AUR-REQ-004 — Alternative-design justification

**Status:** Active

Consequential engineering choices shall identify credible alternatives and preserve
the rationale for the selected design.

### AUR-REQ-005 — Traceable schedule and milestones

**Status:** Active

The project shall maintain a roadmap and live work-tracking system that connect
planned milestones to concrete outcomes and evidence.

### AUR-REQ-006 — Risk management

**Status:** Active

Material technical, domain, integration, personnel, schedule, reproducibility, and
external-dependency risks shall be identified and paired with mitigation, fallback,
or explicit acceptance.

### AUR-REQ-007 — Reproducibility

**Status:** Active

Important AURORA procedures and experiments shall be reproducible from documented
inputs, code, configuration, and dependencies to the extent feasible.

### AUR-REQ-008 — Domain-grounded assumptions

**Status:** Active

Domain-sensitive variables, constraints, interpretations, and validation criteria
shall be grounded in appropriate sources, evidence, or qualified review rather than
invented by the software team.

### AUR-REQ-009 — Explicit claim boundaries

**Status:** Active

AURORA shall distinguish implementation correctness, experimental evidence, simulator
behaviour, and real-field claims. Claims shall not exceed the evidence available.

### AUR-REQ-010 — Closed-loop integration

**Status:** Active

AURORA shall provide an automated closed-loop path connecting reservoir state,
observation, controller decision, safety processing, applied action, subsequent
reservoir evolution, and telemetry.

### AUR-REQ-011 — Observable decisions

**Status:** Active

Important controller actions, safety interventions, experiment conditions, failures,
and relevant provenance shall be observable through structured telemetry/evidence.

### AUR-REQ-012 — Model-mismatch evaluation

**Status:** Active

The safety mechanism shall be evaluated under documented mismatch between the
reduced-order model used for safety decisions and the higher-fidelity numerical
reference used for controlled experiments.

### AUR-REQ-013 — Quantitative comparison

**Status:** Active

Substantive performance/safety claims shall be evaluated using defined metrics and
appropriate baselines/comparators.

### AUR-REQ-014 — Held-out or unseen evaluation

**Status:** Provisional

Where scientifically appropriate, final evaluation shall separate development or
calibration conditions from held-out/unseen conditions and prevent silent retuning
against protected evaluation cases.

Exact split methodology is to be frozen during experiment design.

### AUR-REQ-015 — Presentable demonstration

**Status:** Active

The project shall provide a demonstration that communicates system state, decisions,
safety behaviour, and evidence without requiring a second reader to interpret raw
terminal output.

### AUR-REQ-016 — Individual contribution evidence

**Status:** Active

Each member shall have identifiable engineering contributions and be able to explain
their work, its interfaces, assumptions, evidence, and role in the complete system.

### AUR-REQ-017 — Shared understanding / recoverability

**Status:** Active

No critical subsystem shall depend exclusively on undocumented knowledge held by one
team member.

### AUR-REQ-018 — Data and source provenance

**Status:** Active

External datasets, benchmark models, important derived data, and material assumptions
shall have sufficient provenance to identify their origin, role, and relevant usage
or redistribution constraints.

### AUR-REQ-019 — Failure and robustness evaluation

**Status:** Active

AURORA shall define and test relevant failure or degraded-input conditions and record
expected versus observed behaviour.

### AUR-REQ-020 — Hardware scope

**Status:** Unresolved

The project has not frozen whether a hardware component belongs in the final scope.

No core requirement currently depends on hardware.

## Technical requirements still to be refined

ROADMAP Phases 1–3 must refine, among other things:

- exact observation contract;
- exact action contract;
- control interval;
- objective/reward formulation;
- domain constraints and thresholds;
- CRM formulation and role;
- safety optimization formulation;
- failure semantics;
- simulator/controller interface;
- validation envelope;
- experiment protocol;
- quantitative success thresholds.

Their absence here is intentional. Phase 0 should not turn unresolved technical
questions into fake requirements.
