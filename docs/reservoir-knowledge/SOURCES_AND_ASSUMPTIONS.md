# Sources and Assumptions Register

## Purpose

This document defines how AURORA grounds domain-sensitive statements and records
assumptions.

It is a source-governance document, not a bibliography dump.

## Source hierarchy

Use the most direct authoritative source appropriate to the claim.

### Tier A — primary / authoritative technical sources

Examples:

- official OPM documentation for OPM behaviour and simulator semantics;
- canonical Egg dataset/publication for Egg structure;
- Equinor documentation/licence for Volve provenance and usage conditions;
- primary peer-reviewed work for a specific model/method.

### Tier B — peer-reviewed technical literature

Use for equations, methods, empirical findings, comparisons, and domain relationships
not defined by a primary software/data source.

### Tier C — established textbooks/reference works

Use for stable reservoir-engineering fundamentals.

### Tier D — qualified domain review

Use to review bounded assumptions, interpretations, proposed operating logic, and
questions for which documentary evidence alone is insufficient.

Qualified review supplements evidence. It should not become an undocumented oracle.

### Tier E — AURORA experiments

Use to establish behaviour of AURORA under defined experimental conditions.

AURORA's own experiments do not establish general petroleum-engineering truth.

## Canonical current sources

### Egg Model

Jansen et al., canonical Egg Model dataset / associated publication.

DOI:

https://doi.org/10.4121/uuid:916c86cd-3558-4672-829a-105c62985ab2

Supported use:

- benchmark identity;
- ensemble structure;
- synthetic/channelized nature;
- waterflood configuration;
- canonical well counts;
- benchmark provenance.

### OPM Flow

Official OPM Flow page:

https://opm-project.org/?page_id=19

Official Flow manual page:

https://opm-project.org/?page_id=955

Supported use:

- simulator role/capabilities;
- input/output semantics;
- supported controls/constraints;
- simulator-specific interpretation.

Version-sensitive semantics must be checked against the version actually used by
AURORA.

### Volve

Official Equinor Volve page:

https://www.equinor.com/energy/volve-data-sharing

Local licence copy:

`../../references/volve/Equinor_Volve_Data_Licence.pdf`

Supported use:

- dataset provenance;
- real-field status;
- release purpose;
- licensing/usage context.

The exact semantics of individual workbook columns require the applicable metadata,
documentation, or defensible cross-check. They must not be guessed from column names
alone.

## Assumption states

Every material domain assumption should be identifiable as one of:

- **SOURCE-BACKED** — directly supported by an appropriate source;
- **EXPERIMENTALLY SUPPORTED** — supported within defined AURORA experiments;
- **EXPERT-REVIEWED** — reviewed by a suitably qualified person;
- **PROVISIONAL** — plausible working assumption awaiting stronger support;
- **UNRESOLVED** — insufficient basis for use as a controlled assumption;
- **SUPERSEDED** — retained historically but replaced.

## Assumption record

For a material assumption record:

| Field | Meaning |
|---|---|
| ID | stable identifier |
| Statement | exact assumption |
| Status | state from above |
| Scope | where it applies |
| Evidence | source/experiment/review |
| Risk if wrong | engineering/scientific consequence |
| Resolver | person/task responsible |
| Resolution condition | evidence required to close it |

## Current high-priority unresolved assumptions

The project must not silently invent:

- operational pressure limits;
- injection/production action bounds;
- control interval;
- exact observation availability;
- exact CRM formulation;
- exact mismatch-calibration method;
- reward weights;
- final safety constraints;
- statistical alarm thresholds;
- protected evaluation methodology.

These should become explicit issue/decision records as their roadmap gates are reached.

## Expert review package

A bounded expert review should eventually ask focused questions such as:

1. Are the selected reservoir quantities interpreted correctly?
2. Are the proposed control variables physically meaningful in the chosen experiment?
3. Are candidate constraint types defensible for the stated experiment?
4. Are any simulator quantities being mistaken for real-field measurements?
5. Are the proposed comparisons physically meaningful?
6. Are important confounders or missing variables being overlooked?
7. Are the project's claim boundaries appropriately conservative?
8. Which assumptions most need correction before final evaluation?

The expert should not be asked to validate every simulation run.
