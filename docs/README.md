# AURORA Documentation Guide

This page answers one question:

**Where should I go for the authoritative answer to an AURORA question?**

The repository is organized so that a fact should have one canonical home. Other documents should link to that home instead of creating competing versions.

## Start by question

| Question | Canonical location |
|---|---|
| What is AURORA? | Root `README.md` |
| What principles govern the project? | `PROJECT_PRINCIPLES.md` |
| What must happen from now to completion? | `ROADMAP.md` |
| Which document owns a particular fact? | `docs/project/DOCUMENTATION_AUTHORITY.md` |
| How do I contribute code/docs? | `CONTRIBUTING.md` |
| What am I working on right now? | GitHub Issues / GitHub Project |
| Who owns or backs up a subsystem? | Team/ownership documentation established in Phase 0 |
| What did the professors/course require? | Requirements/feedback traceability established in Phase 0 |
| Why was a consequential decision made? | `docs/decisions/` |
| How does the complete system fit together? | `docs/system-design/` |
| What reservoir knowledge does the project rely on? | `docs/reservoir-knowledge/` |
| What counts as valid/correct behaviour? | `docs/validation/` |
| How is the reservoir simulation handled? | `docs/simulation/` |
| How does the AI controller work? | `docs/ai-controller/` |
| How does the safety controller work? | `docs/safety-controller/` |
| How are data, telemetry, and provenance handled? | `docs/data-and-logging/` |
| How is robustness tested? | `docs/robustness/` |
| How are experiments defined/interpreted? | `docs/experiments/` |
| How will AURORA be demonstrated? | `docs/demo/` |
| Where are formal reports/deliverables developed? | `docs/reports/` |
| Where are meeting records kept? | `docs/meetings/` |
| How should setup/reproducibility automation work? | `docs/development/AUTOMATION_AND_ONBOARDING.md` |
| What feasibility work has already been completed? | `docs/feasibility/` |
| What historical tooling evidence exists? | `docs/tooling/` |

## Documentation rules

1. Prefer links to duplication.
2. Do not turn Discord messages into project truth.
3. Historical documents remain historical; they do not override current canonical specifications.
4. An unresolved technical question should be labelled unresolved rather than silently guessed.
5. Consequential changes should preserve the reason for the change.
6. Evidence and sources should remain traceable to the claims they support.
7. Generated outputs should not be mistaken for specifications.
8. Private/course/internal source material should not be copied into the public repository merely for convenience.

See [`project/DOCUMENTATION_AUTHORITY.md`](project/DOCUMENTATION_AUTHORITY.md) for the formal authority model.
