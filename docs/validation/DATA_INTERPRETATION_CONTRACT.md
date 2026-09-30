# Data Interpretation Contract

## Purpose

Use this template for a substantive issue, experiment, subsystem decision, or milestone
whose outcome depends on interpreting data.

Do not copy the canonical data dictionary into the contract. Link to canonical entries
and document what they mean **for this task**.

---

# DIC-[ID] — [Task / Question]

## 1. Purpose

What question is this data being used to answer?

## 2. Data sources and provenance

For each source:

- raw / measured / simulated / predicted / derived;
- dataset/simulator/model;
- version;
- realization/scenario;
- configuration/run;
- extraction/transformation path.

## 3. Canonical semantics

Link each important variable to `../data-and-logging/DATA_DICTIONARY.md`.

Record any task-specific details:

- units;
- sign convention;
- temporal basis;
- spatial/entity basis;
- missing-value semantics.

## 4. Expectation before observing the result

What behaviour do we expect?

Why?

What evidence supports that expectation?

Avoid writing the expectation after seeing the final result.

## 5. Plausible / normal behaviour

What behaviour would be unsurprising in this task?

What range or pattern is descriptive rather than normative?

## 6. Meaningful change criterion

What makes a change important?

Choose applicable definitions:

- absolute;
- relative;
- persistent;
- baseline-relative;
- statistical;
- engineering;
- physical;
- safety-related.

## 7. Abnormal behaviour

What would be unusual?

What benign explanations must be checked before escalation?

## 8. Concern / alarm criteria

What evidence would justify concern?

What severity levels exist?

What corroborating signals are required?

## 9. Constraints and thresholds

For every relevant boundary, link to
`CONSTRAINT_AND_THRESHOLD_REGISTER.md`.

State whether it is:

- hard physical/domain constraint;
- encoded safety constraint;
- simulator limit;
- experimental bound;
- warning threshold;
- anomaly threshold;
- expected range;
- performance target.

## 10. Cross-variable relationships

Which other quantities must be inspected together?

What relationships are expected?

## 11. Data-quality failure modes

Consider:

- missing data;
- stale data;
- malformed data;
- unit mismatch;
- sign mismatch;
- temporal misalignment;
- reordered entities;
- simulator warnings/failures;
- interpolation;
- normalization;
- outliers;
- future leakage.

## 12. Baseline / comparator

What is the comparator?

Why is it legitimate?

What is held constant?

## 13. Uncertainty

What uncertainty matters here?

How is it represented?

## 14. Interpretation rules

For each important result:

- what would it imply?
- what would it **not** imply?

## 15. Response

What should the system/researcher do?

Possible examples:

- accept;
- log;
- warn;
- reject datum;
- invalidate run;
- fallback;
- intervene;
- stop;
- request review.

## 16. Validation of the interpretation

What supports these rules?

- authoritative documentation;
- literature;
- controlled synthetic test;
- OPM perturbation;
- Volve grounding;
- cross-check;
- expert review.

## 17. Claim boundary

What conclusion may be reported?

What stronger conclusion is explicitly unsupported?

## 18. Evidence

Link exact sources, experiment manifests, code/configuration, and resulting artifacts.

## 19. Open questions

| Question | Resolver | Blocking? | Resolution evidence |
|---|---|---|---|
| | | | |
