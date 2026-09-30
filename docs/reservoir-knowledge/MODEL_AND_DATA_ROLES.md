# Model and Data Roles

## Purpose

AURORA uses several models/data resources with different epistemic roles.

They must not be described as interchangeable evidence.

## Egg

The Egg Model is a synthetic reservoir benchmark.

The canonical TU Delft dataset describes an ensemble of 101 relatively small
three-dimensional realizations of a channelized reservoir under waterflooding, with
eight water injectors and four producers.

AURORA uses Egg because it provides a controlled synthetic setting in which geological
variation and reservoir-control experiments can be studied.

Egg does **not** establish real-field validity.

Canonical dataset DOI:

https://doi.org/10.4121/uuid:916c86cd-3558-4672-829a-105c62985ab2

## OPM Flow

OPM Flow is the project's intended higher-fidelity numerical reservoir-simulation
environment.

OPM describes Flow as a fully implicit black-oil simulator capable of running
industry-standard simulation models and supporting well pressure/rate constraints.

AURORA's wording is deliberately:

**higher-fidelity numerical reference**

not:

**ground truth**

A result reproduced by OPM establishes behaviour of the configured numerical experiment.
It does not by itself establish behaviour of an operating reservoir.

Official documentation:

https://opm-project.org/?page_id=19

https://opm-project.org/?page_id=955

## Egg + OPM

Egg describes the benchmark reservoir/model family.

OPM Flow is the simulator used to execute the relevant configured numerical experiment.

AURORA should preserve the exact Egg realization/input/configuration and OPM environment
needed to reproduce a run.

## Volve

Volve is a real-field data resource released by Equinor.

Equinor describes the release as subsurface and operating data from the Volve field,
which produced from 2008 to 2016.

AURORA currently uses a production-data workbook from that broader release.

Volve's role is grounding, exploratory analysis, interpretation, and potentially
supporting bounded domain questions where the available variables are appropriate.

Volve is **not**:

- the Egg model;
- an OPM realization;
- direct ground truth for an Egg simulation;
- automatic evidence for an Egg safety threshold; or
- proof that a learned AURORA controller is valid for Volve.

Official source:

https://www.equinor.com/energy/volve-data-sharing

The repository also preserves the applicable licence material under
`references/volve/`.

## CRM / CRM-style reduced-order model

A capacitance-resistance-model family is being investigated as AURORA's reduced-order
predictive representation for fast control/safety calculations.

Its project role is fundamentally different from OPM:

- OPM provides the higher-fidelity numerical reference experiment;
- the reduced-order model provides a cheaper simplified prediction used by the control
  architecture;
- the discrepancy between them is itself an experimental quantity.

The exact CRM/CRMIP formulation, inputs, outputs, fitting procedure, assumptions, and
use inside the safety layer remain controlled technical decisions.

Historical feasibility work may discuss candidate formulations. Those discussions do
not freeze the final implementation.

## Learned controller

The learned controller proposes actions based on its defined observation/history.

It does not establish physical validity merely by maximizing reward.

## Safety controller

The safety controller evaluates/modifies a proposed action according to an explicitly
encoded model and constraints.

Its correct claim is therefore conditional:

it can enforce or project against the constraints represented in its mathematical
formulation under its documented assumptions.

It does not provide an unconditional guarantee of real-field safety.

## Role summary

| Resource | Primary role | What it can support | What it cannot establish alone |
|---|---|---|---|
| Egg | Synthetic benchmark / geological ensemble | controlled reservoir experiments | real-field validity |
| OPM Flow | Higher-fidelity numerical reference | numerical reference behaviour | physical ground truth |
| Volve | Real-field data resource | grounding and real-data interpretation | direct Egg truth or arbitrary safety limits |
| CRM/ROM | Simplified predictive model | fast prediction/control calculations | equivalence to full-physics behaviour |
| RL controller | Action proposal | learned sequential policy behaviour | constraint satisfaction by itself |
| Safety layer | Explicit supervisory projection/filter | encoded-constraint handling | unconditional real-world safety |
