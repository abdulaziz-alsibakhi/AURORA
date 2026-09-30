# Course Deliverables and Engineering Inputs

## Purpose

Course deliverables should be generated from AURORA's engineering record rather than
treated as unrelated writing exercises.

The official course material identifies the principal deliverables as the project
proposal, progress report, oral presentation, poster fair, final report, and
project-specific deliverables required by the supervisor.

Dates should be verified against current authoritative course/supervisor information
before being treated as frozen project facts.

## Project proposal

The proposal establishes the planned project.

Its required content includes, at minimum:

- project title, student information, and supervisor information;
- clear project objectives;
- measurable functional and non-functional requirements;
- how progress toward objectives will be measured;
- relevant background and state of the art;
- a description of the intended work;
- relationship to each student's degree program;
- why the team collectively has the required skills;
- methods and their relationship to degree knowledge;
- proposed timetable;
- risks and mitigation;
- required components/facilities; and
- references cited in the text.

Supervisor discussion additionally emphasized system/block diagrams, subsystem
designs, alternative designs and justification, use cases, feasibility, and relevant
cost/resource considerations.

### Primary engineering inputs

- Phase 0 operating model and roadmap;
- Phase 1 domain foundation;
- Phase 2 requirements/validation;
- Phase 3 architecture and alternatives;
- completed feasibility evidence;
- risks/resources;
- team ownership and schedule.

The working LaTeX proposal is in `docs/reports/proposal/`.

## Progress report

The progress report is a midpoint reconciliation against the proposal.

It should:

- reference the original proposal;
- show actual progress;
- predict how the remainder of the project is likely to develop;
- refine the schedule for the final term;
- state necessary variations from the proposal; and
- provide a defensible redefinition where increased knowledge requires one.

This is why AURORA preserves change history rather than rewriting the original plan.

## Oral presentation and demonstration

The oral/demo must communicate the project to a second reader who may not share the
team's detailed implementation context.

AURORA therefore plans presentation-ready visualization and explanation rather than
depending on raw terminal output.

Every member must be prepared to explain the complete system at a high level and
their own contribution in technical depth.

## Poster fair

The poster should communicate:

- the problem;
- the engineering design;
- the central model-mismatch/safety question;
- important alternatives/decisions;
- the experiment design;
- quantitative results;
- limitations; and
- the system/demo in a form suitable for rapid understanding.

## Final report

The final report should be an engineering-design and evidence argument, not a feature
catalogue.

It should reconcile:

    proposal
      -> decisions and deviations
      -> implementation
      -> verification/experiments
      -> results
      -> limitations
      -> final conclusions

The progress report should already provide reusable material for this final record.

## Final video / other project-specific deliverables

Any final video, demonstration artifact, or supervisor-specific deliverable should be
derived from the same canonical architecture, evidence, and result set.

Do not create a separate version of the project's technical truth merely for a
presentation artifact.

## Deliverable traceability

When a formal deliverable makes a technical claim, the supporting evidence should be
traceable back to the repository's canonical specification, experiment, test, or
source.

The deliverable is the communication layer. It is not the sole storage location for
the engineering evidence.
