# AURORA

**Autonomous Upstream Reservoir Optimization and Risk-Aware Agent**

AURORA is a fourth-year Software/Computer Engineering capstone project exploring autonomous, closed-loop reservoir control under partial observability and model uncertainty.

The project combines a learned sequential controller, a reduced-order reservoir model, a constrained safety layer, a higher-fidelity numerical reservoir simulator, experiment telemetry, validation, and a demonstration interface.

> **Status:** Active development. This public repository currently emphasizes architecture, specifications, experiment design, and reproducibility. Implementation will be populated incrementally as components mature.

## The problem

An autonomous controller can propose actions that appear beneficial according to what it has learned, but a learned policy does not inherently guarantee that every proposed action respects operational constraints. A separate safety layer can constrain those actions, but that layer may itself depend on a simplified model that differs from the higher-fidelity environment it is attempting to protect.

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

The intended controller family is recurrent reinforcement learning. The safety subsystem is intended to combine a reduced-order reservoir model with constrained optimization. OPM Flow with the EGG model is being investigated as the higher-fidelity numerical reference environment. Volve is a separate real-field dataset resource and is not interchangeable with the EGG simulation environment.

## Engineering scope

AURORA is a **software and computer engineering system applied to a reservoir-control domain**. Engineering work includes architecture, simulator integration, ML/RL implementation, optimization software, constraint enforcement, model-mismatch characterization, data pipelines, experiment infrastructure, testing, telemetry/provenance, robustness testing, reproducibility, and visualization.

Reservoir engineering supplies application-domain concepts, assumptions, constraints, terminology, and validation context. Domain-sensitive assumptions must be sourced or explicitly marked for review rather than invented by the software team.

## What AURORA does not claim

AURORA does not, by default, claim deployment readiness, validation on an operating reservoir, unconditional physical safety, or replacement of reservoir-engineering judgment. A numerical simulator can provide a higher-fidelity reference environment for controlled experiments without becoming real-field ground truth.

## Workstreams

The project is organized around intuitive workstreams: **System Design**, **Reservoir Knowledge & Validation**, **Reservoir Simulation**, **AI Controller**, **Safety Controller**, **Data & Logging**, **Robustness Testing**, **Experiments & Results**, **Demo & Dashboard**, and **Reports & Presentations**.

## Repository map

| Path | Purpose |
|---|---|
| `docs/` | Architecture, domain knowledge, validation, decisions, meetings and project documentation |
| `src/` | Implementation packages as they are developed |
| `tests/` | Unit, integration, end-to-end and robustness testing |
| `configs/` | Version-controlled runtime/component configuration |
| `data/` | Data documentation and small redistribution-safe samples only |
| `experiments/` | Reproducible experiment definitions, manifests and selected results |
| `artifacts/` | Guidance for generated models, simulator outputs and other large artifacts |
| `references/` | Source and literature tracking |

## Work tracking

GitHub Issues are the canonical work items and GitHub Projects is the project-management layer. The intended board is:

```text
Backlog -> To Do -> In Progress -> Review -> Done
```

A meaningful issue should identify an owner, acceptance criteria, dependencies where relevant, and evidence of completion. Code work should normally connect issue -> branch -> commits -> pull request -> review -> merge.

## Data policy

Do not commit multi-gigabyte raw datasets, large simulator dumps, checkpoints, secrets, or reproducible bulk outputs to normal Git history. The full Volve dataset belongs in appropriate external/local storage. This repository documents its source, structure, use, processing, and—where redistribution permits—small representative samples.

See [`data/README.md`](data/README.md).

## Documentation

Start with [`docs/README.md`](docs/README.md). The documentation is deliberately part of the engineering system: assumptions, interfaces, constraints, experiments, decisions, and validation evidence should remain traceable as implementation evolves.
