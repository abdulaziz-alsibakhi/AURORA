# AURORA

**Autonomous Upstream Reservoir Optimization and Risk-Aware Agent**

AURORA is a fourth-year Software/Computer Engineering capstone project exploring autonomous, closed-loop reservoir control under partial observability and model uncertainty.

The project combines a learned sequential controller, a reduced-order reservoir model, a constrained safety layer, a higher-fidelity numerical reservoir simulator, experiment telemetry, validation, and a demonstration interface.

> **Status:** Active development.
>
> **Current project stage:** Phase 0 — Project Operating System, with proposal, domain, validation, and architecture work beginning in parallel.

## Start here

If you are new to AURORA, use this order:

1. Read this page for the project-level picture.
2. Read [`PROJECT_PRINCIPLES.md`](PROJECT_PRINCIPLES.md) for the rules that govern engineering decisions.
3. Read [`ROADMAP.md`](ROADMAP.md) for the complete execution plan and current phase.
4. Read [`docs/README.md`](docs/README.md) to find the canonical document for a specific question.
5. Read [`CONTRIBUTING.md`](CONTRIBUTING.md) before changing the repository.
6. Use GitHub Issues and the GitHub Project to find current assigned work.

If two documents appear to disagree, do not guess. Follow the authority rules in
[`docs/project/DOCUMENTATION_AUTHORITY.md`](docs/project/DOCUMENTATION_AUTHORITY.md).

## The problem

An autonomous controller can propose actions that appear beneficial according to what it has learned, but a learned policy does not inherently guarantee that every proposed action respects operational constraints.

A separate safety layer can constrain those actions, but that layer may itself depend on a simplified model that differs from the higher-fidelity environment it is attempting to protect.

AURORA therefore focuses on a practical engineering question:

**How should an autonomous reservoir-control system behave when the model used for safety decisions is imperfect?**

## Intended closed loop

```text
Reservoir simulation
        |
        v
   Observation
        |
        v
   AI Controller
        |
        v
 Proposed Action
        |
        v
 Safety Controller
        |
        v
 Applied Action
        |
        v
Reservoir simulation
        |
        +----> Telemetry / validation / next step
```

The intended controller family is recurrent reinforcement learning. The safety subsystem is intended to combine a reduced-order reservoir model with constrained optimization.

OPM Flow with the EGG model is being investigated as the higher-fidelity numerical reference environment. Volve is a separate real-field dataset resource and is not interchangeable with the EGG simulation environment.

Specific observation spaces, action spaces, constraints, control intervals, model formulations, and subsystem contracts are not considered frozen merely because they appear in historical planning material. They become controlled project decisions only after the relevant roadmap gate is completed and the decision is documented.

## Engineering scope

AURORA is a **software and computer engineering system applied to a reservoir-control domain**.

Engineering work includes:

- software architecture and interface design;
- simulator integration;
- machine-learning and reinforcement-learning implementation;
- optimization and safety-filter software;
- model-mismatch characterization;
- data pipelines and provenance;
- experiment infrastructure;
- verification and testing;
- telemetry and observability;
- robustness and failure testing;
- reproducibility; and
- visualization and demonstration software.

Reservoir engineering supplies the application-domain concepts, assumptions, constraints, terminology, and validation context. Domain-sensitive assumptions must be sourced, experimentally justified where appropriate, or explicitly marked for qualified review rather than invented by the software team.

## What AURORA does not claim

AURORA does not, by default, claim:

- deployment readiness on an operating reservoir;
- validation on an operating reservoir;
- unconditional physical safety;
- that a numerical simulator is real-field ground truth; or
- replacement of reservoir-engineering judgment.

Claims must remain proportional to the evidence produced by the project.

## Master execution model

AURORA is organized into thirteen numbered engineering phases:

| Phase | Name |
|---:|---|
| 0 | Project Operating System |
| 1 | Domain Foundation |
| 2 | Requirements & Validation Foundation |
| 3 | System Architecture Freeze |
| 4 | Reproducible Reservoir Environment |
| 5 | Closed-Loop Engineering MVP |
| 6 | Controller & Reduced-Order Modelling |
| 7 | Safety & Model-Mismatch Mechanism |
| 8 | Robustness & Failure Behaviour |
| 9 | Experiment & Evidence System |
| 10 | Integrated Scientific Evaluation |
| 11 | Demo & Human Interpretation |
| 12 | Final Integration & Release |

These are not thirteen isolated waterfalls. Work may proceed in parallel when prerequisites and interfaces permit it.

The authoritative phase definitions, dependencies, gates, and outputs are in [`ROADMAP.md`](ROADMAP.md).

## Continuous project tracks

Four responsibilities run across every applicable phase:

**Documentation** — important assumptions, interfaces, procedures, and results are written as the project evolves.

**Evidence** — engineering and scientific claims remain connected to reproducible evidence.

**Individual contribution** — substantial work remains attributable while avoiding single-person black boxes.

**Course deliverables** — the proposal, progress report, oral presentation/demo, poster, final report, and video are built from the engineering record rather than reconstructed at the deadline.

## Workstreams

Implementation and documentation may be organized around these workstreams:

- System Design
- Reservoir Knowledge & Validation
- Reservoir Simulation
- AI Controller
- Safety Controller
- Data & Logging
- Robustness Testing
- Experiments & Results
- Demo & Dashboard
- Reports & Presentations

Workstreams describe areas of work. The roadmap describes project progression. GitHub Issues describe concrete work items.

## Repository map

| Path | Purpose |
|---|---|
| `docs/` | Canonical project, architecture, domain, validation, decision, meeting, and report documentation |
| `src/` | Implementation packages |
| `tests/` | Unit, integration, end-to-end, regression, and robustness tests |
| `configs/` | Version-controlled runtime and experiment configuration |
| `data/` | Data documentation and redistribution-safe project data |
| `experiments/` | Reproducible experiment definitions, manifests, and selected results |
| `artifacts/` | Policy and guidance for generated models, simulator outputs, and large artifacts |
| `references/` | Source, literature, licence, and reference tracking |

See [`docs/README.md`](docs/README.md) for the question-oriented documentation map.

## Work tracking

GitHub Issues are the canonical work items. GitHub Projects represents current execution status.

The intended workflow is:

```text
Backlog -> To Do -> In Progress -> Review -> Done
```

A meaningful issue should eventually identify:

- the intended outcome;
- a primary owner;
- a backup/reviewer where appropriate;
- prerequisites or dependencies;
- acceptance criteria; and
- evidence required for completion.

Code work should normally follow:

```text
Issue -> temporary branch -> implementation + verification
      -> pull request -> review -> merge to main -> issue complete
```

The detailed contribution model is defined in [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Data and artifact policy

Do not commit secrets, unnecessary bulk simulator output, large reproducible dumps, checkpoints, or other unsuitable artifacts to normal Git history.

Whether a dataset belongs in Git depends on size, redistribution rights, provenance, and reproducibility needs rather than a blanket rule.

The official Volve production workbook currently preserved by AURORA is intentionally version-controlled together with its licence/provenance documentation. Large or unnecessary source packages and generated simulator outputs remain external or reproducible from documented procedures.

See [`data/README.md`](data/README.md) and [`artifacts/README.md`](artifacts/README.md).

## Current next step

The project is currently establishing **Phase 0 — Project Operating System** while beginning proposal work in parallel.

The immediate objective is to make the repository sufficiently navigable and traceable that a teammate can determine:

- what AURORA is;
- why it exists;
- what phase it is in;
- what must happen next;
- what they own;
- what they need to read;
- how to contribute;
- what counts as done;
- where decisions came from; and
- where evidence belongs

without depending on private knowledge held by one team member.
