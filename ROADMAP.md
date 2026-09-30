# AURORA Master Roadmap

## 1. Purpose

This document is the canonical long-range execution plan for AURORA.

It defines the project's engineering phases, major dependencies, exit gates, and expected outputs. GitHub Issues and GitHub Projects represent the live execution state of this roadmap; they do not replace it.

The roadmap is deliberately more stable than the task board. Phase status may change continuously. The phase structure changes only through deliberate project-level change control.

## 2. Execution model

AURORA uses a gated but parallel execution model.

A phase gate means that a downstream claim or dependency must not assume work is complete before its required gate has been satisfied. It does not mean every team member must stop until the entire previous phase is finished.

Parallel work is encouraged where interfaces and prerequisites permit it.

The high-level dependency spine is:

    Phase 0: Project Operating System
                    |
          +---------+---------+
          |         |         |
          v         v         v
       Phase 1   Phase 2   Phase 3
       Domain    Req/Val    Architecture
          \         |         /
           +-------- + -------+
                    |
                    v
                 Phase 4
          Reservoir Environment
                    |
                    v
                 Phase 5
            Closed-Loop MVP
                    |
             +------+------+
             |             |
             v             v
          Phase 6        Phase 7
        Controller       Safety
             \             /
              +-----------+
                    |
                    v
                 Phase 8
                Robustness
                    |
                    v
                 Phase 9
          Experiment/Evidence
                    |
                    v
                Phase 10
        Integrated Evaluation
                    |
                    v
                Phase 11
           Demo/Interpretation
                    |
                    v
                Phase 12
        Final Integration/Release

Documentation, evidence, individual-contribution records, and course deliverables run continuously across applicable phases.

---

## Phase 0 — Project Operating System

### Objective

Make AURORA navigable, governable, traceable, and executable as a five-person engineering project.

### Subphases

0.1 Define source-of-truth and document authority rules.
0.2 Freeze the master roadmap structure.
0.3 Establish repository navigation and onboarding.
0.4 Define contribution and Git workflow.
0.5 Define primary-owner and backup/reviewer responsibilities.
0.6 Capture course and supervisor requirements as traceable engineering inputs.
0.7 Initialize GitHub Issues/Projects/milestones from the roadmap.
0.8 Establish controlled change and decision recording.

### Exit gate

A teammate unfamiliar with the current state can determine what AURORA is, why it exists, where authoritative information lives, what the project must do next, what they own, how to contribute, and what counts as complete without relying on undocumented knowledge held by one person.

### Major outputs

- root project front door;
- master roadmap;
- documentation authority map;
- contribution workflow;
- team/ownership model;
- Definition of Done;
- requirements and feedback traceability;
- decision/change-control mechanism; and
- initialized execution board.

---

## Phase 1 — Domain Foundation

### Objective

Establish enough defensible reservoir-domain understanding to design, interpret, and validate the software system without inventing petroleum-engineering assumptions.

### Subphases

1.1 Reservoir fundamentals relevant to AURORA.
1.2 Waterflooding and reservoir-control fundamentals.
1.3 Injection/production wells and control quantities.
1.4 Variables, units, terminology, and physical interpretation.
1.5 EGG benchmark role and limitations.
1.6 OPM Flow role and limitations.
1.7 Volve dataset role, contents, provenance, and limitations.
1.8 CRM fundamentals and intended reduced-order role.
1.9 Canonical glossary and source mapping.
1.10 Bounded expert-review package and domain questions.

### Exit gate

No domain-sensitive concept required by the proposed AURORA design exists solely as an unexplained or unsourced team assumption.

### Major outputs

- reservoir-domain guide;
- variable/terminology dictionary;
- source and assumption register;
- EGG/OPM/Volve/CRM role definitions; and
- expert-review brief.

---

## Phase 2 — Requirements & Validation Foundation

### Objective

Define what AURORA must do and what evidence is required to call its behaviour correct, acceptable, unsafe, invalid, or out of scope.

### Subphases

2.1 Functional requirements.
2.2 Non-functional requirements.
2.3 Domain-sensitive requirements.
2.4 Canonical variables, units, and schemas.
2.5 Operating/experimental envelope.
2.6 Encoded constraints and their provenance.
2.7 Validation rules and levels of correctness.
2.8 Success metrics and evaluation criteria.
2.9 Explicit claim boundaries and non-claims.

### Exit gate

Every important future result has a defined interpretation, validation basis, and claim boundary.

### Major outputs

- requirements specification;
- validation specification;
- variable dictionary;
- constraint/source mapping;
- success metrics; and
- claim-boundary documentation.

---

## Phase 3 — System Architecture Freeze

### Objective

Define stable subsystem responsibilities and interfaces so implementation can proceed in parallel without producing incompatible components.

### Subphases

3.1 Closed-loop system architecture.
3.2 Component responsibilities and boundaries.
3.3 Observation contract.
3.4 Action contract.
3.5 Component APIs/data contracts.
3.6 Telemetry and provenance contract.
3.7 Failure semantics and containment.
3.8 Alternative-design analysis.
3.9 Architecture Decision Records for consequential choices.

### Exit gate

Subsystems can be implemented independently against documented, reviewed interfaces, and consequential architectural choices have explicit justification.

### Major outputs

- architecture specification;
- system/component diagrams;
- interface contracts;
- observation/action contracts;
- failure semantics; and
- ADRs.

---

## Phase 4 — Reproducible Reservoir Environment

### Objective

Make the numerical reservoir reference environment reproducible from a fresh clone using documented and increasingly automated procedures.

### Subphases

4.1 Environment/dependency diagnostics.
4.2 EGG authoritative-source acquisition.
4.3 Source verification and preparation.
4.4 OPM Flow installation/setup validation.
4.5 Deterministic reference simulation.
4.6 Output extraction and normalization.
4.7 Standardized reservoir adapter.
4.8 Guided automation through the AURORA tooling path.

### Exit gate

A teammate can move from a fresh clone and documented prerequisites to a verified reservoir run and standardized AURORA-readable output without relying on the historical workspace.

### Major outputs

- reproducible setup/run procedure;
- verified simulator inputs;
- environment diagnostics;
- reservoir adapter;
- standardized output; and
- reproducibility evidence.

---

## Phase 5 — Closed-Loop Engineering MVP

### Objective

Demonstrate the complete AURORA software control loop before depending on sophisticated learned/control components.

### Subphases

5.1 Reservoir adapter.
5.2 Observation pipeline.
5.3 Deterministic/simple controller baseline.
5.4 Safety-controller interface.
5.5 Action application.
5.6 Telemetry and provenance capture.
5.7 Closed-loop orchestration.
5.8 End-to-end verification.

### Exit gate

The following loop executes automatically and reproducibly:

    reservoir
      -> observation
      -> controller
      -> safety layer
      -> applied action
      -> reservoir
      -> telemetry/logging
      -> next step

### Major outputs

- executable closed loop;
- baseline controller;
- safety interface;
- telemetry records; and
- end-to-end tests/evidence.

---

## Phase 6 — Controller & Reduced-Order Modelling

### Objective

Develop and evaluate the decision-making and reduced-order modelling components required for sequential reservoir control.

### Subphases

6.1 Simple/control baseline.
6.2 CRM implementation and verification.
6.3 Reinforcement-learning environment.
6.4 PPO baseline.
6.5 Partial-observation formulation.
6.6 Recurrent controller candidate.
6.7 Fair controller comparison.
6.8 Closed-loop controller integration.

### Exit gate

Controller/model choices used by later experiments are supported by reproducible evidence and defined evaluation criteria rather than assumption.

### Major outputs

- verified CRM path;
- RL environment;
- controller baselines;
- recurrent-controller implementation where justified;
- comparison evidence; and
- integrated controller interface.

---

## Phase 7 — Safety & Model-Mismatch Mechanism

### Objective

Implement and evaluate AURORA's defining research mechanism: constrained safety decisions when the reduced-order safety model differs from the higher-fidelity reference environment.

### Subphases

7.1 Nominal operational constraints.
7.2 Safety optimization formulation.
7.3 Nominal safety-filter baseline.
7.4 Paired reduced-order/reference evaluation.
7.5 Model-mismatch characterization.
7.6 Uncertainty/calibration method.
7.7 Mismatch-aware constraint handling.
7.8 Intervention logging and analysis.

### Exit gate

The complete mismatch-aware safety mechanism runs end-to-end, its assumptions are explicit, and its behaviour can be compared against defined baselines.

### Major outputs

- nominal safety filter;
- mismatch dataset/evidence;
- calibration/uncertainty mechanism;
- mismatch-aware safety filter; and
- intervention telemetry.

---

## Phase 8 — Robustness & Failure Behaviour

### Objective

Determine how AURORA behaves when observations, models, software components, or experimental assumptions fail.

### Subphases

8.1 Observation noise.
8.2 Missing, delayed, or stale observations.
8.3 Model perturbations.
8.4 Out-of-distribution/unseen conditions.
8.5 Software/component faults.
8.6 Fallback, containment, and recovery behaviour.
8.7 Robustness regression tests.
8.8 Reserved team scope pending unresolved project decisions.

### Important unresolved item

The role of a possible hardware component and Timur's final specialization is intentionally **not decided by this roadmap version**. It remains parked pending the relevant supervisor/team decision. No core AURORA dependency may assume either outcome until that decision is recorded.

### Exit gate

Important failure modes have documented expected behaviour, reproducible test cases, and observable outcomes.

### Major outputs

- fault model;
- robustness scenarios;
- failure-handling behaviour;
- regression tests; and
- robustness evidence.

---

## Phase 9 — Experiment & Evidence System

### Objective

Make every important engineering/scientific claim reproducible and traceable to exact inputs, code, configuration, and outputs.

### Subphases

9.1 Experiment manifest format.
9.2 Data/code/configuration provenance.
9.3 Random seeds and reproducibility controls where applicable.
9.4 Baseline/comparison matrix.
9.5 Calibration/validation/test separation where applicable.
9.6 Batch experiment runner.
9.7 Failure and negative-result retention.
9.8 Figure/table/result lineage.

### Exit gate

Every important reported number or figure can be traced to a reproducible experiment definition and its relevant code, data, and configuration.

### Major outputs

- experiment specification;
- manifests;
- provenance system;
- batch runner;
- baseline matrix; and
- evidence lineage.

---

## Phase 10 — Integrated Scientific Evaluation

### Objective

Evaluate whether the complete AURORA system supports its intended claims under the frozen experimental protocol.

### Subphases

10.1 Freeze evaluation protocol.
10.2 Held-out/unseen evaluation.
10.3 Controller comparisons.
10.4 Safety-filter comparisons.
10.5 Ablations.
10.6 Production/extraction metrics where defensible.
10.7 Pressure/constraint metrics.
10.8 Violation/intervention metrics.
10.9 Economic metrics where defensible.
10.10 Statistical analysis and uncertainty.
10.11 Limitations and negative results.

### Exit gate

Every substantive project claim is quantitatively supported, rejected, or explicitly left unresolved, with limitations proportional to the evidence.

### Major outputs

- final experiment suite;
- quantitative results;
- ablations;
- statistical analysis;
- figures/tables; and
- limitations record.

---

## Phase 11 — Demo & Human Interpretation

### Objective

Make AURORA understandable and inspectable by a technically capable reader who has not followed the implementation.

### Subphases

11.1 Demonstration narrative and UX.
11.2 Reservoir-state visualization.
11.3 Controller-action visualization.
11.4 Safety intervention visualization.
11.5 Model-mismatch/uncertainty visualization.
11.6 Telemetry and provenance views.
11.7 Experiment replay/comparison.
11.8 Failure/robustness demonstration.

### Exit gate

A second reader can understand what the system did, why it acted, what the safety layer changed, what evidence supports the result, and what the result does not prove without interpreting raw terminal output.

### Major outputs

- demonstration interface;
- replay/comparison workflow;
- presentation-ready visualizations; and
- demo runbook.

---

## Phase 12 — Final Integration & Release

### Objective

Produce a coherent, reproducible final engineering system and evidence package suitable for the capstone's final evaluation.

### Subphases

12.1 Full-system integration.
12.2 Regression/reproducibility verification.
12.3 Documentation freeze and consistency audit.
12.4 Final evidence package.
12.5 Individual-contribution evidence.
12.6 Adversarial/second-reader rehearsal.
12.7 Release candidate.
12.8 Final archival/release record.

### Exit gate

The technical system, evidence, documentation, demonstration, and course deliverables tell one internally consistent and defensible story.

### Major outputs

- final integrated system;
- reproducibility record;
- final evidence package;
- release artifact; and
- final documentation baseline.

---

## 3. Continuous deliverables track

Course deliverables are not independent engineering phases. They are produced continuously from the project record.

### Project proposal

Built primarily from Phases 0–3 plus completed feasibility work. It defines what AURORA proposes to build, why, how, with what alternatives, risks, resources, schedule, and validation strategy.

### Progress report

Compares actual progress and deviations against the approved proposal and roadmap.

### Oral presentation and demonstration

Uses the integrated system and evidence available by the presentation milestone, with enough completed core functionality to demonstrate the project's architecture and engineering contribution.

### Poster fair

Communicates the mature project, major design decisions, quantitative results, and demonstration.

### Final report and video

Represent the final engineering record, evidence, results, limitations, and individual/team contributions.

---

## 4. Roadmap governance

The following are treated as stable baseline decisions unless deliberately changed:

- this roadmap's phase structure;
- the distinction between roadmap, live work tracking, and technical specifications;
- the requirement for evidence-backed completion;
- the source-of-truth model;
- traceability expectations;
- primary/backup understanding;
- controlled recording of consequential decisions.

Technical details that have not passed their corresponding phase gate are **not frozen by implication**.

Examples include exact observation vectors, action vectors, constraints, control intervals, hyperparameters, model structures, calibration methods, and experiment protocols.

Those decisions should be investigated, justified, recorded, and then controlled at the appropriate phase.

---

## 5. Definition of roadmap completion

A phase is not complete because its planned calendar window has passed.

A phase is complete when its exit gate and required evidence have been satisfied.

If implementation moves ahead before a prerequisite gate is fully complete, the dependency must be explicit and the downstream work must not silently convert an unresolved assumption into a project fact.
