# Documentation Authority and Source-of-Truth Model

## Purpose

AURORA must not accumulate multiple competing answers to the same project question.

This document defines which artifacts are authoritative for which kinds of information and how conflicts are resolved.

## Core rule

**A fact should have one canonical home. Other documents link to it rather than independently redefining it.**

## Authority by information type

| Information | Canonical authority |
|---|---|
| Project identity, high-level purpose, navigation | Root `README.md` |
| Stable engineering principles | `PROJECT_PRINCIPLES.md` |
| Long-range execution phases, dependencies, gates | `ROADMAP.md` |
| Current task status | GitHub Issues / GitHub Project |
| Contribution/Git/PR workflow | `CONTRIBUTING.md` |
| Major architectural structure and interfaces | `docs/system-design/` |
| Consequential design decisions and rationale | `docs/decisions/` |
| Domain terminology and grounded reservoir knowledge | `docs/reservoir-knowledge/` |
| Validation rules and claim boundaries | `docs/validation/` |
| Simulation procedures/contracts | `docs/simulation/` |
| AI-controller specification | `docs/ai-controller/` |
| Safety-controller specification | `docs/safety-controller/` |
| Data/provenance/telemetry specification | `docs/data-and-logging/` |
| Robustness specification | `docs/robustness/` |
| Experiment definitions and interpretation rules | `docs/experiments/` |
| Demo specification | `docs/demo/` |
| Formal course reports/deliverables | `docs/reports/` |
| Historical meeting record | `docs/meetings/` |
| External literature/source tracking | `references/` |
| Data provenance and dataset-specific policy | `data/` |

Some Phase 0 authorities are intentionally still being established. Until their canonical document exists, the corresponding item is unresolved rather than implicitly owned by a historical document.

## Evidence hierarchy

Different sources answer different questions. They must not be collapsed into one authority level.

### External requirements

Official course material and explicit supervisor instructions define external project obligations.

They are inputs to AURORA's requirements and deliverables. They are not rewritten to match later project preferences.

### Canonical project specifications

Approved repository specifications define the team's current engineering intent.

### Decision records

Decision records explain why consequential choices were made or changed. They preserve history; they do not replace the current specification.

### Evidence

Tests, experiments, simulator outputs, source documents, and validated analyses support or challenge project claims.

Evidence does not silently redefine requirements or architecture.

### Historical/internal material

Old handbooks, presentations, planning documents, chat discussions, scratch notes, and superseded specifications are useful historical inputs.

They are not authoritative merely because they were written earlier or shared with the team.

## Conflict resolution

When two artifacts disagree:

1. Identify what kind of fact is in conflict.
2. Find the canonical authority for that information type.
3. Check whether a later approved decision record intentionally changed it.
4. Check the supporting external requirement/evidence where relevant.
5. If the conflict cannot be resolved from approved material, mark it unresolved.
6. Do not silently choose whichever version is more convenient.

## Stable baseline versus controlled evolution

AURORA distinguishes three kinds of project state.

### Stable baseline

Examples:

- repository/navigation philosophy;
- source-of-truth model;
- roadmap phase structure;
- traceability model;
- contribution workflow once approved;
- Definition-of-Done philosophy;
- decision-record mechanism.

These should not change casually.

### Controlled technical evolution

Examples:

- observation/action contracts;
- constraints;
- algorithms;
- subsystem interfaces;
- validation methodology;
- experimental protocol;
- architecture.

These may evolve as evidence improves, but consequential changes must preserve rationale and affected dependencies.

### Live execution state

Examples:

- issue status;
- assigned work;
- branch/PR state;
- blockers;
- current experiment runs;
- milestone progress.

These are expected to change continuously.

## Relationship to formal reports

Formal reports describe the project at a particular point in time.

A proposal does not permanently override the current engineering specification after the project legitimately evolves. Instead:

- the proposal records the approved plan at proposal time;
- current canonical documentation records the current project state;
- decision/change records explain important deviations;
- the progress/final reports reconcile actual work against earlier plans.

This preserves both historical accuracy and current clarity.

## Private and public information

The public repository is the canonical home for engineering information that is appropriate to publish.

Private course materials, private supervisor communications, raw meeting transcripts, internal discussions, or redistribution-restricted sources should not be committed publicly merely to make them convenient to reference.

Instead, public canonical documents should capture the resulting project requirement, decision, or sourced conclusion without unnecessarily publishing the private source itself.

## Change rule

A consequential change is not complete when a file is silently edited.

Where appropriate, the change should identify:

- what changed;
- why it changed;
- supporting evidence or requirement;
- affected interfaces/requirements/milestones;
- migration or follow-up work; and
- the decision record or pull request that approved it.

The detailed change-control workflow will be established during Phase 0.
