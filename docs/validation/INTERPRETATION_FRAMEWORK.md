# Data Interpretation Framework

## Purpose

This document answers:

**Once AURORA has a number, what does that number mean?**

Interpretation occurs at three levels.

## Level 1 — Canonical meaning

Shared across the project:

- definition;
- units;
- sign convention;
- source;
- spatial/temporal basis;
- raw/predicted/derived status;
- valid/invalid states;
- relationships;
- authoritative references.

Canonical meaning belongs primarily in the data dictionary and reservoir-domain
documentation.

## Level 2 — Subsystem/context meaning

The same physical source can have different significance to different subsystems.

### OPM / Egg reference simulation

Questions include:

- Is the simulator run valid?
- Is the quantity physically/numerically plausible?
- What well/control mode produced it?
- Was the requested control actually effective?
- Is a warning material?
- Could the behaviour be a configuration or numerical artefact?
- Is the result consistent across related signals?

### Learned controller

Questions include:

- Is this quantity actually observable to the policy?
- Has it been normalized/scaled?
- Is history available?
- Is it delayed or noisy?
- Does it leak future/reference information?
- Is the representation stable across training/evaluation?
- Does the reward respond as intended?

### CRM / safety controller

Questions include:

- What quantity is being predicted?
- Is the prediction aligned in time and units with the reference?
- What does the residual mean?
- Which error direction matters to the selected constraint?
- Is the current case within the model/calibration envelope?
- What uncertainty is represented?
- Why did the safety layer intervene?

### Telemetry / provenance

Questions include:

- Where did the value originate?
- Is it raw or derived?
- Which run/configuration/timestep produced it?
- Is it missing, stale, malformed, reordered, or unit-inconsistent?
- Can the exact decision be reconstructed?

## Level 3 — Task/milestone meaning

Each substantive data-heavy issue should instantiate a Data Interpretation Contract.

The contract records what the data means **for that task** without redefining its
canonical semantics.

## Interpretation pipeline

    raw/source data
        -> semantic understanding
        -> structural/data-quality validation
        -> transformation
        -> contextual interpretation
        -> domain validation
        -> constraint/significance interpretation
        -> system response
        -> experiment conclusion
        -> report claim

## Meaningful change

A change is not "meaningful" until the criterion is defined.

Possible criteria include:

- absolute magnitude;
- relative magnitude;
- persistence over time;
- comparison with baseline;
- uncertainty interval;
- statistical criterion;
- engineering consequence;
- physical consequence;
- constraint consequence.

The applicable criterion must be chosen before interpreting the result where practical.

## Abnormal versus concerning

AURORA uses the following reasoning discipline:

    unusual
        does not automatically mean
    physically concerning
        does not automatically mean
    encoded safety violation
        does not automatically mean
    real-world unsafe

Each transition requires evidence.

## Benign explanations

Before escalating an unexpected value, consider applicable alternatives:

- unit conversion;
- sign convention;
- changed control mode;
- report-step/control-step mismatch;
- normalization;
- stale data;
- missing-data imputation;
- numerical solver behaviour;
- changed realization;
- configuration change;
- derived-metric definition;
- legitimate transient response.

## Response ladder

A task may define responses such as:

1. accept;
2. accept and log;
3. warn;
4. request corroborating signal;
5. reject datum;
6. mark run invalid;
7. apply fallback;
8. safety intervention;
9. stop experiment;
10. require human/domain review.

The response must match the evidence. "Looks weird" is not a response specification.

## Interpretation lineage example

    OPM well pressure
        -> extracted value
        -> unit/identity/time validation
        -> normalized controller feature
        -> CRM prediction of corresponding quantity
        -> aligned OPM/CRM residual
        -> safety-relevant discrepancy statistic
        -> constraint margin
        -> QP intervention
        -> realized OPM outcome
        -> experiment metric
        -> bounded claim

Every stage has a different meaning even though several stages may still be casually
described as "pressure."

## No retrospective threshold invention

AURORA should avoid looking at final results and then inventing a threshold that makes
the preferred method look successful.

Important thresholds/metrics should be frozen before protected final evaluation where
scientifically appropriate.
