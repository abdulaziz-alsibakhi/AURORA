# Constraint and Threshold Register

## Purpose

This register prevents unrelated numerical boundaries from being treated as if they
all mean "safety limit."

No numerical operational threshold is frozen by this initial foundation.

## Threshold classes

### Hard physical/domain constraint

A boundary claimed to represent a physically or operationally unacceptable condition.

**Evidence burden:** high.

Requires appropriate domain evidence and, where necessary, qualified review.

### Encoded safety-controller constraint

A mathematical constraint represented in AURORA's safety formulation.

This may be inspired by a domain requirement but remains a property of the modeled
system unless stronger validation exists.

### Simulator control/limit

A control or limit defined by the reservoir simulation configuration.

This describes the configured numerical experiment.

### Experimental bound

A boundary deliberately imposed to define the experimental search/control space.

It must not automatically be called a physical safety limit.

### Warning threshold

A value that triggers attention or additional checks without itself establishing
invalidity or violation.

### Statistical anomaly threshold

A criterion for unusual behaviour relative to a defined statistical baseline/model.

Unusual does not automatically mean physically unsafe.

### Expected range

A descriptive range expected under a defined source/context.

It is not automatically a constraint.

### Performance target

A desired objective or success criterion.

Failure to reach it is not automatically a safety violation.

## Required record fields

Before a material threshold is used, record:

| Field | Meaning |
|---|---|
| ID | stable identifier |
| Quantity | canonical data-dictionary entry |
| Class | one class above |
| Numerical value/rule | explicit rule |
| Units | explicit |
| Direction | upper/lower/two-sided/etc. |
| Scope | where it applies |
| Source | evidence/provenance |
| Rationale | why it exists |
| Response | what happens when crossed |
| Uncertainty treatment | if applicable |
| Status | proposed/reviewed/frozen/superseded |
| Claim boundary | what crossing means and does not mean |

## Current register

| ID | Quantity | Class | Value | Status | Notes |
|---|---|---|---|---|---|
| CTR-001 | TBD selected safety quantity | encoded safety-controller constraint | UNRESOLVED | UNRESOLVED | Must be justified before safety experiments are frozen |
| CTR-002 | controller action bounds | experimental/domain-dependent bound | UNRESOLVED | UNRESOLVED | Must follow action-space decision |
| CTR-003 | anomaly/warning criteria | warning/statistical threshold | UNRESOLVED | UNRESOLVED | Define only where operationally useful |

## Prohibited shortcut

A historical Volve range, an Egg baseline range, a percentile, or a convenient round
number must not be promoted to a hard physical/safety constraint merely because the
number is available.

The source must support the interpretation being claimed.
