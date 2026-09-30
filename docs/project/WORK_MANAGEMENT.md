# AURORA Work Management

> **New here? Start here:**
>
> **README → Project → My Work → To Do → Issue → Branch → PR → Review → Done**
>
> Your assigned **To Do** issue tells you what outcome is needed and how to prove it.

## How we work

AURORA uses **lightweight Agile + milestone-driven Kanban + V-model-inspired verification/validation traceability**.

- milestones define meaningful outputs;
- issues define small, verifiable work;
- Kanban shows current status;
- CI checks what machines can check;
- another person reviews changes before `main`;
- important results trace to requirements, decisions, and evidence.

We are intentionally not strict Scrum, Waterfall, or a classical V-model.

## What do I work on?

Open **AURORA Execution → My Work**.

| State | Meaning |
|---|---|
| **Backlog** | Known work. Do not start yet. |
| **To Do** | Ready and assigned. Work comes from here. |
| **In Progress** | Actively being worked on. |
| **Review** | Ready for independent review. |
| **Done** | Accepted, reviewed, and evidenced. |

**Do not randomly pull from Backlog.**

`blocked` is a label, not a state. Record why you are blocked and what would unblock you.

## Normal task flow

1. Open your highest-priority assigned **To Do** issue.
2. Read its objective, acceptance criteria, dependencies, and evidence.
3. Move it to **In Progress**.
4. Create a short-lived branch.
5. Do the work and add appropriate tests.
6. Open a PR linked to the issue.
7. Let CI run.
8. Move to **Review** when ready.
9. Another teammate reviews it.
10. Merge only after required checks and approval pass.
11. Move to **Done** when acceptance criteria and evidence are satisfied.

Nothing assigned? Check the current milestone with the team. Do not invent work.

## Good issues

A normal issue describes **one meaningful, reviewable outcome**, usually small enough to report on within about one working week.

Good:

- `🌊 Establish reproducible OPM reference run`
- `🧠 Implement PPO baseline`
- `🔌 Define controller-safety interface`

Bad:

- `Work on OPM`
- `Do AI`
- separate tickets for trivial edits

If the work materially expands or changes a controlled decision, stop and create/link the necessary follow-up.

## Workstream key

| | Workstream |
|---|---|
| 🌊 | Reservoir / OPM |
| 🧠 | AI Controller |
| 🛡️ | Safety / QP |
| 📊 | Data / Telemetry |
| 🧪 | Robustness / Testing |
| 🔌 | Integration / Architecture |
| 📝 | Deliverables / Documentation |
| 🎬 | Demo / Presentation |

Use at most one leading workstream emoji. It does not represent priority or status.

## Done means demonstrated

As applicable, **Done** means:

- acceptance criteria satisfied;
- appropriate tests/checks pass;
- required evidence exists;
- affected docs/interfaces are updated;
- independent review is complete;
- PR is merged when repository changes are involved.

CI verifies encoded checks. It does **not** establish scientific or physical validity.

## Engineering traceability

For consequential work:

**Need → Requirement → Alternatives/Decision → Implementation → Verification → Validation/Evidence → Claim**

Do not silently change controlled requirements, architecture, interfaces, scientific assumptions, or experiment protocols.

## Weekly meeting

Before the supervisor meeting, update your active issue with:

- result/evidence;
- blocker or decision needed;
- next step.

The Project is the status report. Meeting notes preserve decisions, professor feedback, blockers, and actions.

## Where do I go?

| I need to... | Go to... |
|---|---|
| know what to do now | **Project → My Work** |
| review work | **Project → Review Needed** |
| prepare for the meeting | **Project → This Week** |
| understand the plan | `ROADMAP.md` |
| contribute | `CONTRIBUTING.md` |
| understand AURORA | root `README.md` |
| understand a major choice | linked decision/ADR |
| understand a result | linked validation/evidence |

## The test

A contributor should always be able to answer:

**What is mine? What outcome is required? How do I prove it? Who reviews it? Is it Done?**
