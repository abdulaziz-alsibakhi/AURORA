# AURORA Glossary

This glossary defines project terminology at the level required for shared team
understanding.

Detailed variable semantics belong in `../data-and-logging/DATA_DICTIONARY.md`.

## A

### Action

A controller output representing a proposed control decision.

AURORA distinguishes a **proposed action** from the **applied action** after safety
processing and simulator/interface handling.

## B

### BHP — Bottom-Hole Pressure

Pressure associated with a well at the bottom-hole reference used by the simulator or
data source.

A value labelled BHP must still identify source, units, well, time, and whether it is a
target, limit, prediction, or realized output.

## C

### Constraint

A boundary represented in a specific mathematical, simulator, experimental, or
operational context.

AURORA never assumes that every "limit" is the same kind of constraint.

### CRM — Capacitance-Resistance Model

A family of reduced-order/data-driven reservoir models investigated by AURORA for
simplified dynamic prediction.

The exact AURORA formulation is not yet frozen.

### Cumulative quantity

A quantity accumulated over time, such as cumulative production or injection.

It must not be interpreted as an instantaneous rate.

## E

### Egg Model

A synthetic channelized reservoir benchmark distributed as an ensemble of geological
realizations and commonly used for reservoir-simulation/control research.

AURORA uses Egg as a controlled synthetic benchmark, not a real field.

## H

### Higher-fidelity numerical reference

A numerical model/simulator used as the more detailed experimental reference relative
to a reduced-order model.

For AURORA, OPM Flow + the configured Egg experiment serves this role.

This term deliberately does not mean physical ground truth.

## I

### Injector

A well configured to introduce fluid into the simulated reservoir.

### Interpretation

The process of determining what a datum/result means in context, including comparator,
expected behaviour, uncertainty, significance, and legitimate conclusions.

## M

### Model mismatch

A difference between behaviour/prediction of models representing the same relevant
experimental quantity or response.

AURORA is especially interested in safety-relevant discrepancy between a reduced-order
model and the higher-fidelity numerical reference.

## O

### Observation

Information made available to the learned controller at a control step.

An observation is not necessarily the complete simulator state.

### OPM Flow

An open-source reservoir simulator from the Open Porous Media project used by AURORA
as the intended higher-fidelity numerical reference environment.

### Operating / experimental envelope

The documented conditions within which an AURORA interpretation, test, or claim is
intended to apply.

It is not automatically equivalent to the safe operating envelope of a real field.

## P

### Partial observability

A condition in which the controller does not have direct access to the complete state
needed to perfectly characterize the environment.

### Permeability

A rock/property concept related to the ability of porous material to transmit fluid.

### Porosity

The fraction of bulk rock volume represented by pore space.

### Producer

A well configured to remove reservoir fluids.

## Q

### QP — Quadratic Program

An optimization problem with a quadratic objective and suitable constraints.

AURORA is investigating a QP-style safety projection/filter. The final mathematical
formulation is not frozen by this glossary.

## R

### Rate

A quantity expressed per unit time.

Always identify phase/stream, well/field scope, source, sign convention, and units.

### Realization

One particular model instance from an ensemble, such as a geological realization of
the Egg benchmark.

### Reduced-order model (ROM)

A simplified model intended to represent selected system dynamics at lower complexity
than the higher-fidelity reference.

## S

### Safety controller / safety layer

A supervisory component that checks or modifies a proposed action according to
explicitly represented constraints/model assumptions.

The word "safety" in the component name does not imply unconditional physical safety.

### Saturation

Fraction of pore volume occupied by a particular fluid phase.

### Significance

A context-dependent judgment about whether a difference/result matters.

AURORA distinguishes statistical, engineering, physical, and safety significance.

## T

### Telemetry

Structured records that make system state, decisions, transformations, interventions,
failures, and provenance observable and reconstructable.

## V

### Validation

Evidence-based checking that an artifact, result, or interpretation satisfies defined
criteria for a stated scope.

### Volve

A real North Sea field dataset released by Equinor.

AURORA treats Volve as a separate grounding/data resource, not as Egg/OPM ground truth.

## W

### Waterflooding

A reservoir-management process involving water injection and production behaviour.

AURORA studies a waterflood control setting through numerical experiments.
