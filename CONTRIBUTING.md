# Contributing to AURORA

## Purpose

AURORA uses a lightweight but traceable engineering workflow.

Important work should not exist only on one person's laptop, in Discord, or in an
unreviewed document.

The normal path is:

    requirement / roadmap outcome
        -> GitHub issue
        -> temporary work branch
        -> implementation + verification + evidence
        -> pull request
        -> review
        -> merge to main
        -> issue complete

## Before starting work

1. Find or create the GitHub Issue representing the work.
2. Confirm the intended outcome and acceptance criteria.
3. Identify relevant requirement IDs where applicable.
4. Check prerequisites and dependent interfaces.
5. Confirm primary ownership and appropriate reviewer/backup.
6. Read the canonical documentation for the affected subsystem.

If the issue requires an unresolved technical decision, resolve or explicitly isolate
that decision before silently encoding an assumption in code.

## Branches

`main` is the only permanent development branch.

Use short-lived, descriptive branches tied to the work rather than to a person's
name.

Examples:

    simulation/egg-opm-setup
    controller/rppo-baseline
    safety/nominal-qp
    validation/domain-rules
    docs/proposal-architecture

Avoid permanent per-person branches.

## Working changes

Keep a change focused enough that a reviewer can understand why it exists.

Where applicable:

- add or update tests;
- preserve experiment/configuration evidence;
- update canonical documentation;
- identify changed assumptions;
- avoid committing secrets or unnecessary generated data;
- do not manually rewrite experimental outputs to make them look cleaner.

## Commits

Prefer meaningful commits that describe the engineering change.

Conventional-style messages are encouraged where natural, for example:

    feat: add reservoir observation adapter
    fix: preserve well ordering in telemetry
    test: add safety-filter regression case
    docs: define reservoir validation rules
    chore: update reproducibility tooling

Do not optimize contribution evidence around commit count.

## Pull requests

A substantial pull request should make it easy to answer:

1. What changed?
2. Why was the change needed?
3. Which issue/requirement does it address?
4. How was it verified?
5. What evidence was produced?
6. Did assumptions, interfaces, constraints, or limitations change?

If a consequential decision changed, link the relevant ADR or change record.

## Review

Review is intended to catch integration, reasoning, reproducibility, and
single-person-knowledge problems, not merely formatting errors.

A reviewer should consider:

- acceptance criteria;
- interface compatibility;
- tests/checks;
- evidence;
- assumptions;
- documentation;
- reproducibility;
- downstream consequences.

Sensitive changes involving domain constraints, validation methodology, experimental
protocol, protected evaluation data, major interfaces, or safety behaviour should not
be changed casually by one person without meaningful review.

## Merge

Merge to `main` only when the applicable Definition of Done is satisfied.

The authoritative Definition of Done is:
`docs/project/DEFINITION_OF_DONE.md`.

After merge:

- ensure the issue reflects the outcome;
- preserve relevant evidence;
- update dependent work if the change affects it.

## Documentation

Follow `docs/project/DOCUMENTATION_AUTHORITY.md`.

A fact should have one canonical home. Prefer linking to the canonical specification
rather than maintaining multiple independent copies.

## Consequential decisions

Follow `docs/project/CHANGE_CONTROL.md`.

Use an ADR for decisions whose rationale future contributors need to preserve.

## Data and generated artifacts

Do not commit secrets, unnecessary simulator dumps, large reproducible artifacts, or
redistribution-restricted material.

Dataset-specific policy belongs under `data/`; generated-artifact policy belongs
under `artifacts/`.

## Asking for help / blockers

A blocker should become visible rather than remaining in private chat.

Use the relevant GitHub issue to record the technical blocker and what is needed to
continue. Communication may happen elsewhere, but the durable engineering state
belongs in GitHub.

## Definition of Done

Completion is evidence-based, not calendar-based.

See `docs/project/DEFINITION_OF_DONE.md`.
