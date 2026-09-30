# AURORA Validation Specification

## 1. Purpose

This specification defines the validation philosophy that future subsystem and
experiment specifications must instantiate.

It intentionally does not invent numerical reservoir thresholds.

## 2. Levels of correctness

### Level 1 — Implementation correctness

Question:

**Did the software do what its implementation/interface specification says?**

Evidence may include:

- unit tests;
- integration tests;
- schema validation;
- deterministic checks;
- numerical sanity checks;
- interface-contract tests.

Passing Level 1 says nothing by itself about petroleum-domain validity.

### Level 2 — Experimental correctness

Question:

**Was the intended experiment executed correctly and reproducibly?**

Evidence may include:

- exact configuration;
- input manifests;
- realization identity;
- seeds;
- simulator version;
- controller/safety configuration;
- baseline/comparator definition;
- protected evaluation discipline;
- artifact lineage.

### Level 3 — Domain plausibility and grounding

Question:

**Is the interpretation defensible within the stated reservoir-engineering context?**

Evidence may include:

- authoritative documentation;
- peer-reviewed literature;
- controlled perturbation tests;
- cross-variable consistency;
- known physical relationships;
- qualified expert review.

This level is stronger than "the plot looks reasonable."

### Level 4 — Real-field validity

Question:

**Has the system been shown valid for an operating reservoir and its real operational
conditions?**

AURORA does not assume this level is achieved.

Neither OPM consistency nor Volve analysis alone establishes it.

## 3. Validation dimensions

Important results should be evaluated across applicable dimensions.

### Structural

- correct schema;
- expected dimensions;
- required fields;
- finite values;
- identifiers resolve.

### Temporal

- timestamps/control steps align;
- no accidental future leakage;
- correct lag/window;
- stale data detectable;
- cumulative/rate quantities not confused.

### Unit/sign

- units explicit;
- conversions controlled;
- sign convention known;
- incompatible quantities not compared.

### Provenance

- source known;
- transformation known;
- version/configuration known;
- derived value reproducible.

### Numerical

- solver/run status acceptable;
- no silent NaN/Inf propagation;
- tolerances defined where needed;
- numerical failure not interpreted as physical behaviour.

### Domain

- quantity has correct physical meaning;
- trends/relationships have a defensible interpretation;
- operating assumptions are documented;
- simulator-specific artefacts considered.

### Statistical

Where statistical inference is used:

- population/sample is identified;
- dependence structure is considered;
- uncertainty is reported;
- multiple comparisons/selection effects are considered where relevant;
- statistical significance is not substituted for engineering importance.

### Comparative

A comparison must define:

- baseline;
- changed factor;
- held-constant factors;
- metric;
- aggregation;
- uncertainty;
- legitimate scope of conclusion.

## 4. Significance categories

AURORA distinguishes:

### Statistical significance

Evidence that an observed difference is unlikely under a defined statistical null/model.

### Engineering significance

A difference large enough to materially affect system behaviour or the project question.

### Physical significance

A difference that matters to interpretation of reservoir behaviour.

### Safety significance

A difference relevant to an explicitly defined safety/constraint decision.

These categories may overlap but are not synonyms.

## 5. Result states

A validation process may classify a result as:

- `VALID_FOR_SCOPE`
- `VALID_WITH_WARNING`
- `INSUFFICIENT_EVIDENCE`
- `INVALID_DATA`
- `INVALID_EXPERIMENT`
- `OUTSIDE_ENVELOPE`
- `NUMERICAL_FAILURE`
- `DOMAIN_REVIEW_REQUIRED`

Machine-readable names may evolve during architecture work, but the distinctions should
be preserved.

## 6. Cross-variable validation

Important signals should not always be interpreted independently.

Where appropriate, validation should check relationships among:

- requested and realized controls;
- injection and production response;
- pressure and rate behaviour;
- rate and cumulative quantities;
- CRM predictions and OPM reference quantities;
- proposed and applied actions;
- constraint state and intervention;
- simulator warnings and suspicious outputs.

## 7. Baseline requirement

Statements such as:

- improved;
- degraded;
- stable;
- large;
- small;
- accurate;
- safer;
- robust;

require an explicit comparator or definition.

## 8. Uncertainty requirement

AURORA must distinguish at least:

- stochastic variability;
- geological/realization variability;
- model discrepancy;
- measurement/data uncertainty where applicable;
- numerical effects;
- uncertainty introduced by limited sample size.

Do not collapse all uncertainty into one unlabeled error bar.

## 9. Failure retention

Failed or invalid runs relevant to evaluation should not silently disappear.

Experiment infrastructure should preserve enough information to determine:

- what failed;
- where;
- under which configuration;
- whether the run belongs in the analysis population; and
- why it was included/excluded.

## 10. Claim boundary

Every substantive conclusion should answer:

1. What exact evidence supports this?
2. Under what model/data/configuration?
3. Against what comparator?
4. Over what population/realizations/time?
5. What uncertainty applies?
6. What does the result **not** establish?

## 11. Validation envelope

For AURORA, "validation envelope" means the explicitly documented scope within which a
validation rule or claim is intended to apply.

It may include:

- simulator/version;
- reservoir/model family;
- realizations;
- control configuration;
- observation availability;
- action bounds;
- time horizon;
- perturbation/failure regime;
- model calibration conditions.

It is a project validation concept.

It must not be represented as a certified safe operating envelope for a real field.

## 12. Exit condition for a final metric

A metric intended to support a final project claim should not be frozen until:

- semantics are defined;
- units/aggregation are defined;
- baseline is defined;
- expected direction/interpretation is stated;
- uncertainty treatment is defined;
- invalid-run treatment is defined;
- significance is defined;
- claim boundary is stated; and
- the metric is linked to a requirement/research question.
