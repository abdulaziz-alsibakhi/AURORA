# F2 — Egg Dataset Technical Audit

**Project:** AI-Enhanced Sequential Dependency Optimization in Physical and Conceptual Spaces (AURORA)  
**Feasibility stage:** F2  
**Verdict:** **CONDITIONAL PASS**

## 1. Purpose

This audit determines whether the locally acquired Egg Model package contains
the reservoir structure, geological variability, wells, controls, physical
properties, schedule information, and response quantities required to justify
proceeding with AURORA's executable full-physics feasibility testing.

F2 is a static dataset audit. It does not claim that OPM Flow has successfully
executed the model. Executability and controlled perturbation are tested in F3.

## 2. Dataset Identification and Integrity

The Egg package was obtained and integrity-checked during F1. The archive
extracts successfully and contains simulator/model representations including
Eclipse, MRST, MoReS, AD-GPRS, and a directory of permeability realizations.

The extracted working dataset contains the Eclipse model used as the primary
candidate for OPM Flow compatibility testing.

## 3. Grid and Active Cells

The Eclipse deck defines a grid of:

- NX = 60
- NY = 60
- NZ = 7
- Total Cartesian cells = 25,200

The ACTNUM data contains 25,200 binary entries:

- Active cells = 18,553
- Inactive cells = 6,647
- Other ACTNUM values = 0

The ACTNUM size therefore matches the Cartesian grid exactly.

## 4. Reservoir Properties

The supplied Eclipse model contains the principal static and fluid information
required for an oil-water reservoir simulation, including:

- METRIC unit system
- oil and water phases
- grid geometry
- active-cell definition
- porosity
- net-to-gross
- directional permeability
- oil PVT data
- water PVT data
- rock property specification
- SWOF relative-permeability/saturation table
- equilibrium initialization

The supplied deck specifies uniform porosity of 0.2 and NTG of 1.

This audit records raw deck values where simulator keyword semantics or units
still require authoritative OPM-reference verification. F2 does not infer
unsupported positional meanings.

## 5. Base Permeability

The base/reference permeability representation explicitly provides PERMX.

The deck then applies:

- COPY PERMX to PERMY
- COPY PERMX to PERMZ
- MULTIPLY PERMZ by 0.1

After resolving these operations, the base model contains complete
25,200-cell X, Y, and Z directional permeability fields.

## 6. Geological Ensemble

The package contains 100 files named PERM1_ECL.INC through
PERM100_ECL.INC.

All 100 supplied files were parsed and semantically resolved.

Result:

- Supplied PERM files checked: 100
- Complete/valid after resolution: 100
- Invalid: 0

PERM54 initially appeared structurally different because it contains only an
explicit PERMX array. Inspection showed that it uses COPY operations to create
PERMY and PERMZ and then multiplies PERMZ by 0.1. Once those Eclipse operations
are resolved, PERM54 also contains complete 25,200-cell X/Y/Z permeability
fields.

Therefore the PERM54 size difference is not treated as evidence of corruption.

The local evidence proves 100 supplied permeability-realization files plus the
supplied base/reference permeability field. F2 does not independently claim
that these are 101 statistically independent geological realizations; that
interpretation should be tied to authoritative Egg documentation.

## 7. Wells

The main Eclipse deck defines 12 wells:

- 8 water injectors
- 4 oil producers

Injector locations:

| Well | I | J |
|---|---:|---:|
| INJECT1 | 5 | 57 |
| INJECT2 | 30 | 53 |
| INJECT3 | 2 | 35 |
| INJECT4 | 27 | 29 |
| INJECT5 | 50 | 35 |
| INJECT6 | 8 | 9 |
| INJECT7 | 32 | 2 |
| INJECT8 | 57 | 6 |

Producer locations:

| Well | I | J |
|---|---:|---:|
| PROD1 | 16 | 43 |
| PROD2 | 35 | 40 |
| PROD3 | 23 | 16 |
| PROD4 | 43 | 18 |

The main-deck COMPDAT records open the listed wells through layers 1–7.

A separate COMPDAT.INC file also exists in the package, but it is not referenced
by Egg_Model_ECL.DATA. The active candidate Eclipse deck contains its own
COMPDAT section, so the two must not be conflated.

## 8. Baseline Controls

The supplied producer baseline uses BHP control with raw deck value 395.

The supplied injector schedule defines all eight injectors as:

- phase: WATER
- status: OPEN
- control mode: RATE
- baseline rate raw value: 79.5
- additional raw control/constraint value: 420

The exact positional interpretation and units of relevant control fields will
be verified against the selected OPM Flow reference during F3 rather than
inferred from memory.

The existence of explicit injector-rate controls is important for AURORA
because it provides a legitimate simulator control variable that can later be
perturbed during F3.

## 9. Schedule

The supplied schedule contains:

- 120 timestep entries
- 30 days per timestep
- total simulated baseline duration = 3,600 days

This provides a long sequential reservoir-management trajectory.

The supplied 30-day schedule is a property of the baseline Egg case. F2 does
not declare that AURORA's final RL/control decision interval must necessarily
be 30 days.

## 10. Requested Simulator Responses

The supplied SUMMARY section requests:

- FOPR — field oil production rate
- FWPR — field water production rate
- FWIR — field water injection rate
- WOPR — oil production rate for PROD1–PROD4
- WWPR — water production rate for PROD1–PROD4
- WWIR — water injection rate for INJECT1–INJECT8
- FOPT — cumulative field oil production
- FWPT — cumulative field water production
- FWIT — cumulative field water injection
- WLPR — liquid production rate for PROD1–PROD4

These requests demonstrate that the deck is configured to request important
production/injection response quantities.

However, requested SUMMARY keywords are not treated as proof that OPM
successfully generates readable output files. That is an F3 execution test.

## 11. Pressure and State Information

No explicit pressure SUMMARY request was observed in the supplied SUMMARY
section.

This is an open issue rather than an F2 failure.

AURORA's final observation and safety architecture may require pressure/state
information. F3 must determine whether suitable quantities are available from
OPM-generated restart/summary outputs or whether explicit pressure-related
SUMMARY requests must be added.

F4 will subsequently map the final available quantities against every AURORA
input/output requirement.

## 12. Train / Calibration / Final-Test Feasibility

The presence of 100 validated supplied permeability realization files provides
a substantial geological ensemble for later experimental partitioning.

The final train/calibration/final-test split is not frozen by F2. It should be
defined only after confirming simulator compatibility and the precise
relationship between the supplied base/reference case and the documented Egg
ensemble.

No realization should cross experimental partitions once the split is frozen.

## 13. Problems and Resolutions

### PERM54 size anomaly

**Observed:** PERM54 was approximately one third the size of neighboring
realization files and a naive numeric parser returned approximately one third
as many numeric tokens.

**Investigation:** PERM54 explicitly defines PERMX and uses Eclipse COPY
operations to derive PERMY and PERMZ, followed by a PERMZ multiplier of 0.1.

**Resolution:** semantic parsing resolves complete 25,200-cell PERMX, PERMY and
PERMZ fields. PERM54 is therefore not rejected as corrupt.

### Initial semantic-audit false negatives

An early audit script incorrectly reported several included/derived properties
as missing and generated four false well records.

Those results were parser defects, not dataset defects. The evidence was
corrected using direct source inspection and semantic handling. The final F2
artifacts supersede those preliminary parser interpretations.

## 14. Remaining Questions

The following are deliberately not closed by F2:

1. Does the selected OPM Flow version execute the supplied Egg case?
2. What are the authoritative OPM units/semantics of the relevant control
   fields?
3. Which pressure/state quantities are actually generated and programmatically
   accessible?
4. Can a legitimate injector-control perturbation be applied successfully?
5. Does that perturbation cause a measurable reservoir response?
6. Can Python extract the required outputs reproducibly?
7. Does the final set of available quantities satisfy every AURORA
   observation/action/safety requirement?
8. Are the reservoir-engineering abstractions and assumptions defensible?

Questions 1–6 primarily belong to F3, question 7 to F4, and question 8 to F5.

## 15. AURORA Compatibility Assessment

Static dataset evidence supports proceeding because the package contains:

- reservoir geometry and active-cell structure
- physical oil-water simulation properties
- geological permeability variation
- explicit injection and production wells
- explicit controllable water-injection rates
- sequential scheduling
- production and injection response requests
- sufficient supplied geological cases to justify further ensemble testing

No static-data defect has been found that currently makes the proposed
AURORA experiment impossible.

This does **not** yet establish full end-to-end AURORA data sufficiency.
Executable simulator behavior and final input-output traceability remain
mandatory gates.

## 16. Verdict

**CONDITIONAL PASS**

F2 finds the Egg package structurally and informationally suitable to advance
to OPM execution testing.

The condition is that F3 must demonstrate:

- successful OPM execution,
- programmatic output extraction,
- usable state/pressure information,
- legitimate control modification, and
- measurable physical response to that modification.

F4 must then demonstrate that the confirmed simulator quantities cover the
AURORA architecture's required inputs and outputs.

Therefore:

**Proceed to F3. Do not yet declare the overall AURORA feasibility study GO.**
