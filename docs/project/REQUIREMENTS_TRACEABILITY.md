# Requirements Traceability

## Purpose

AURORA should be traceable in both directions:

    Why are we doing this?
        -> requirement / supervisor or course need
        -> roadmap phase
        -> GitHub issue
        -> implementation/documentation
        -> verification/evidence
        -> result
        -> proposal/report/demo

and:

    Where did this result come from?
        -> experiment/test
        -> code/configuration/data
        -> issue/decision
        -> requirement
        -> project objective or external need

This file owns project-level traceability structure. GitHub owns live issue status.

## Current traceability matrix

| Requirement | Primary roadmap phase(s) | Expected evidence / artifact | Deliverable relevance |
|---|---|---|---|
| AUR-REQ-001 Objectives | 0, 2 | objectives + measurable criteria | Proposal, progress, final |
| AUR-REQ-002 Functional/NFRs | 2 | requirements specification | Proposal, final |
| AUR-REQ-003 Program relevance | 0–3 | subsystem/method mapping | Proposal, oral, final |
| AUR-REQ-004 Alternatives | 3, 6, 7 | ADRs + alternative analysis | Proposal, final |
| AUR-REQ-005 Schedule/milestones | 0 | roadmap + GitHub execution state | Proposal, progress |
| AUR-REQ-006 Risks | 0–12 | risk register + mitigations/outcomes | Proposal, progress, final |
| AUR-REQ-007 Reproducibility | 4, 9, 12 | setup/run instructions, manifests, tests | Progress, final |
| AUR-REQ-008 Domain grounding | 1, 2 | domain guide, sources, validation spec, review | Proposal, final |
| AUR-REQ-009 Claim boundaries | 2, 10 | validation spec + limitations | Proposal, oral, final |
| AUR-REQ-010 Closed loop | 3–5 | E2E loop + test evidence | Progress, demo, final |
| AUR-REQ-011 Observability | 3, 5, 9, 11 | telemetry/provenance + demo | Demo, final |
| AUR-REQ-012 Model mismatch | 7, 10 | paired experiments + mismatch evidence | Oral, poster, final |
| AUR-REQ-013 Quantitative comparison | 9, 10 | baseline matrix + metrics/results | Oral, poster, final |
| AUR-REQ-014 Held-out evaluation | 9, 10 | frozen protocol + protected evaluation | Final |
| AUR-REQ-015 Presentable demo | 11 | dashboard/replay/demo runbook | Oral, poster |
| AUR-REQ-016 Individual evidence | all | issues, PRs, evidence ledger, presentations | All assessed work |
| AUR-REQ-017 Shared understanding | 0–12 | backups, docs, reviews, handoff readiness | Meetings, oral |
| AUR-REQ-018 Provenance | 1, 4, 9 | source manifests/licences/experiment lineage | Proposal, final |
| AUR-REQ-019 Robustness | 8, 10 | fault scenarios + regression/evaluation | Demo, final |
| AUR-REQ-020 Hardware scope | unresolved | supervisor/team decision record | TBD |
| AUR-REQ-021 Data semantics/interpretation | 1, 2, 3, 9, 10 | data dictionary + interpretation contracts + validation evidence | Proposal, demo, final |

## Known supervisor concern mapping

| Concern | Requirement response |
|---|---|
| How do we know reservoir-related results are meaningful? | AUR-REQ-008, 009, 013 |
| How is this SE/CSE engineering? | AUR-REQ-003 |
| Can someone else continue a member's work? | AUR-REQ-016, 017 |
| Why this design rather than another? | AUR-REQ-004 |
| Why should a reader believe the results? | AUR-REQ-007, 008, 009, 013, 014, 018 |
| Demo should not be unexplained terminal output | AUR-REQ-011, 015 |
| Hardware may be bolted on | AUR-REQ-020 |

## Issue linkage

When GitHub issues are initialized, meaningful issues should include relevant
requirement IDs.

Example:

    Requirements:
    - AUR-REQ-008
    - AUR-REQ-018

This provides stable linkage without encoding live issue numbers into the requirement
definition itself.

## Evidence linkage

As experiments and tests mature, this matrix should link to canonical evidence or
experiment manifests rather than duplicating result values here.

This file answers "where is the evidence?" It should not become the evidence itself.
