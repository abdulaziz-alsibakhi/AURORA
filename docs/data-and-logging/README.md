# Data, Logging, and Provenance

This workstream makes AURORA experiments reconstructable.

The canonical semantic registry is [`DATA_DICTIONARY.md`](DATA_DICTIONARY.md).

Interpretation and validation rules live under [`../validation/`](../validation/).

## Provenance principle

A run should eventually identify, as applicable:

- simulator/model version;
- reservoir realization/scenario;
- controller configuration;
- safety configuration;
- experiment configuration;
- random seeds;
- timestamps and control/report steps;
- source observations;
- transformed observations;
- proposed actions;
- safety decisions/interventions;
- applied actions;
- relevant constraint state;
- model predictions;
- mismatch diagnostics;
- failures/warnings;
- summary metrics;
- input/configuration hashes; and
- Git commit.

## Distinguish stages

Do not overwrite one semantic stage with another.

For example:

    proposed action
        != safety-filtered action
        != simulator-requested action
        != realized reservoir response

Similarly:

    raw value
        != normalized value
        != model prediction
        != residual
        != derived constraint quantity

## Data-quality states

Important pipelines should be able to distinguish, where relevant:

- present and valid;
- missing;
- stale;
- malformed;
- unit-inconsistent;
- temporally misaligned;
- out of expected schema;
- numerically non-finite;
- simulator-invalid;
- rejected by validation.

The exact machine-readable telemetry schema is frozen during architecture/integration
work, not by this foundation document.
