# Change Control

## Purpose

AURORA must be able to evolve without losing the reasoning behind its design.

The rule is:

**AURORA has one canonical plan. Changes to that plan are decisions, not accidents.**

## What can change normally

Live execution state changes constantly and does not require an ADR:

- issue status;
- assignments;
- branches and pull requests;
- implementation details that do not alter an interface or requirement;
- bug fixes;
- experiment runs;
- ordinary documentation clarification.

## What requires deliberate change control

A consequential change should be recorded when it materially changes one or more of:

- project scope;
- roadmap structure or phase gates;
- system architecture;
- subsystem responsibility;
- canonical interface/schema;
- observation or action contract;
- domain-sensitive constraint;
- validation methodology;
- experimental protocol or protected test set;
- major algorithm/design choice;
- externally committed proposal assumption;
- safety-related behaviour;
- project claim boundary.

## Decision process

For a consequential change:

1. State the current decision or assumption.
2. State the proposed change.
3. Identify why change is necessary.
4. Record supporting evidence, requirement, or newly discovered constraint.
5. Identify credible alternatives where relevant.
6. Identify affected requirements, interfaces, phases, experiments, and deliverables.
7. Record the decision in an ADR when the change is architectural or otherwise
   important enough to require durable rationale.
8. Update the canonical specification.
9. Update dependent issues/documentation.
10. Preserve historical evidence rather than rewriting it to make the new decision
    appear to have always been the plan.

## Unresolved decisions

An unresolved decision should remain explicitly unresolved.

Do not resolve uncertainty by copying an old handbook, chat message, or prototype
implementation into a canonical specification.

Examples currently include:

- Timur's final specialization and the role, if any, of hardware;
- technical contracts that ROADMAP Phase 3 deliberately leaves open; and
- calendar details not yet verified against authoritative course/supervisor material.

## Proposal deviations

The proposal records the plan at proposal time.

If the project later changes legitimately, the current canonical documents should be
updated through this process. The progress/final reports should then explain the
variation from the proposal rather than silently modifying history.

## Emergency fixes

A defect that threatens repository integrity or blocks the team may be corrected
quickly, but consequential implications still need to be documented afterward.

Speed does not remove the requirement for traceability.
