# Reservoir Domain Guide

## 1. Purpose

This guide defines the minimum shared reservoir-domain understanding required by
AURORA.

It is intentionally bounded. The project is a Software/Computer Engineering capstone,
not a substitute for professional reservoir-engineering analysis.

The guide therefore concentrates on concepts that directly affect:

- simulation;
- observations;
- actions;
- reduced-order modelling;
- controller behaviour;
- safety filtering;
- telemetry;
- validation; and
- interpretation of experimental results.

## 2. Reservoir state

A reservoir simulation represents the evolution of fluids in porous rock.

Important AURORA concepts include:

### Porosity

Porosity describes the fraction of bulk rock volume represented by pore space.

Porosity is not the same thing as permeability. A rock may contain pore space without
providing the same ease of fluid flow as another rock with similar porosity.

### Permeability

Permeability characterizes the ability of porous material to transmit fluid under a
pressure gradient.

For AURORA, permeability is especially important because geological heterogeneity can
change communication between injectors and producers and therefore change the response
to a control action.

### Pressure

Pressure is a state/control-relevant physical quantity, but the word "pressure" alone
is insufficient.

AURORA must distinguish, where applicable:

- reservoir/grid pressure;
- well bottom-hole pressure;
- other simulator pressure quantities;
- measured or historical pressure;
- model-predicted pressure;
- normalized pressure used by ML;
- pressure residual/error; and
- a pressure-derived constraint expression.

These quantities are not interchangeable.

### Saturation

Saturation describes the fraction of pore volume occupied by a fluid phase.

A saturation value must be interpreted together with its phase, location, simulator
definition, and context.

### Rates and cumulative quantities

A rate describes change per unit time. A cumulative quantity integrates production or
injection over time.

AURORA must not confuse an instantaneous or interval rate with a cumulative quantity.

## 3. Wells

AURORA's current experimental direction involves production and injection wells.

A producer removes reservoir fluids.

An injector introduces fluid into the reservoir as defined by the simulation/control
configuration.

A well may operate under different control modes. Therefore, the existence of a
requested target does not by itself prove that the target was the effective limiting
control at every instant.

The exact simulator semantics must be checked against the applicable OPM Flow
configuration and output.

## 4. Waterflooding

Waterflooding uses water injection as part of reservoir pressure/support and displacement
strategy.

For AURORA, the software-engineering significance is that changing injection decisions
can affect later reservoir and producer behaviour.

Those effects:

- are dynamic rather than instantaneous;
- may be delayed;
- may differ across wells;
- depend on reservoir connectivity and heterogeneity;
- may be only partially visible to a controller; and
- may differ between a reduced-order model and a higher-fidelity simulator.

This is one reason recurrent control and model-mismatch evaluation are relevant project
questions.

## 5. Control and observation are different concepts

A simulator may expose much more state than a realistic controller should observe.

Therefore AURORA distinguishes:

- simulator-internal state;
- quantities extracted for validation;
- controller observations;
- safety-model inputs;
- telemetry;
- report/demo quantities.

A variable's existence in OPM output does not automatically authorize it as an RL
observation.

Observation design must consider partial observability and future-information leakage.

## 6. Physical meaning versus software representation

The same underlying concept can appear in several software representations.

Example lineage:

    OPM pressure
        -> extracted physical quantity
        -> validated/cleaned value
        -> normalized ML feature
        -> CRM-predicted pressure
        -> OPM-minus-CRM residual
        -> uncertainty/calibration quantity
        -> QP constraint expression
        -> safety intervention diagnostic

Each arrow changes the interpretation.

AURORA must preserve enough provenance to identify which representation a value belongs
to.

## 7. Interpretation discipline

A large number is not automatically bad.

An unusual number is not automatically physically concerning.

A physically concerning result is not automatically an encoded AURORA safety violation.

A constraint violation inside a model does not automatically establish real-field
unsafe behaviour.

Interpretation must identify:

1. the quantity;
2. the reference context;
3. the comparator;
4. expected behaviour;
5. uncertainty;
6. significance category;
7. corroborating evidence; and
8. the conclusion that the evidence actually supports.

## 8. Current unresolved domain decisions

The following are intentionally not frozen by this guide:

- exact controller observation vector;
- exact controller action vector;
- control interval;
- reward/objective formulation;
- numerical operational limits;
- exact CRM formulation;
- exact QP formulation;
- mismatch-calibration method;
- protected evaluation split; and
- numerical success thresholds.

These become controlled decisions only when their roadmap gates are completed and their
evidence is recorded.

## 9. Sources

Canonical source records and source hierarchy are maintained in
`SOURCES_AND_ASSUMPTIONS.md`.

Variable-specific definitions belong in
`../data-and-logging/DATA_DICTIONARY.md`.
