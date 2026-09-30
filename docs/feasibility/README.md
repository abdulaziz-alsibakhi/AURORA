# AURORA Feasibility Investigation

This directory preserves the structured feasibility investigation performed
before full AURORA implementation.

The purpose of this work was to turn major project risks and supervisor
concerns into explicit, testable engineering questions rather than relying on
assumptions.

## Reports

| Report | Purpose |
|---|---|
| F1 | Data source and access verification |
| F2 | Egg dataset technical audit |
| F3 | OPM Flow + Egg execution test |
| F4 | Data traceability analysis |
| F5 | Domain validation investigation |
| F6 | State-of-the-art and novelty investigation |
| F7 | Volve real-field grounding investigation |
| G0 | Consolidated feasibility go/no-go decision |

## Evidence

`evidence/` contains machine-generated or directly captured evidence supporting
the reports.

Examples include:

- source manifests and cryptographic hashes;
- Egg model properties and well information;
- OPM execution results;
- baseline-versus-perturbed simulation comparisons;
- Volve schema and missingness analysis;
- well activity and role analysis;
- temporal coverage;
- lag/correlation investigations;
- CRM-IP exploratory results.

The reports and evidence should be interpreted together.

## Reproducibility note

Some feasibility analyses were performed interactively during the initial
investigation. Their resulting evidence and source artifacts were preserved,
but the original one-off analysis scripts were not all retained.

AURORA should progressively replace those one-off analyses with committed,
reproducible scripts whenever the result becomes part of the production
experimental pipeline.

Historical evidence must not be silently regenerated or altered merely to make
it appear reproducible after the fact.

## Relationship to implementation

These reports establish feasibility and design evidence.

They are not substitutes for the implementation, validation specification,
experiment harness, automated tests, or final evaluation required by AURORA.
