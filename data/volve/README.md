# Volve Data

This directory contains the Volve production dataset used by AURORA for
real-field grounding, data characterization, reduced-order modelling
investigations, and validation-related analysis.

## Original source artifact

The canonical source workbook is:

`original/Volve production data.xlsx`

This file is preserved as an **immutable source artifact**.

Do not manually edit, clean, normalize, interpolate, filter, reorder, or
overwrite this workbook.

Any transformed data used by AURORA must be produced as a separate derived
artifact by code.

### Verified artifact

- File size: `2,342,595 bytes`
- SHA-256:
  `514d4e38763e09be7fbad12313429909b9799b1a6ec999bf5f36e0df1b6c9cae`

The F7 audit recorded:

- `Daily Production Data`: 15,634 rows × 24 columns
- `Monthly Production Data`: 527 raw rows × 10 columns

See:

`../../docs/feasibility/F7_volve_grounding_report.md`

and:

`../../docs/feasibility/evidence/F7/`

for the existing characterization and grounding evidence.

## Data workflow

AURORA follows:

    immutable source data
            |
            v
    reproducible processing code
            |
            v
    derived / processed data
            |
            v
    experiments and models

Team members should therefore read from the original workbook but should not
modify it in place.

## Licence and attribution

The Volve data is provided by Equinor and the former Volve licence partners
under the applicable Volve data licence.

A copy of the licence used during AURORA's feasibility investigation is
preserved at:

`../../references/volve/Equinor_Volve_Data_Licence.pdf`

Use and redistribution of the data must comply with those terms.

The dataset must not be presented in a misleading, distorted, or incorrect
manner.

## Important distinction

Volve is AURORA's real-field grounding dataset.

It is not the same thing as the Egg synthetic reservoir model used with
OPM Flow for controlled simulation experiments.

Those resources have different roles in the AURORA evaluation architecture.
