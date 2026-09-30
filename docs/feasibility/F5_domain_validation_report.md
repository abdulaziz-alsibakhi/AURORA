# F5 — Reservoir Engineering Assumptions & Domain Validation Report

## Verdict: CONDITIONAL PASS

## 1. Objective

F5 tests whether AURORA's reservoir-engineering assumptions are defensible enough to proceed without silently turning a software/control experiment into physically meaningless reservoir engineering.

This report separates:

- facts supported by the Egg benchmark and OPM/Egg evidence;
- modelling choices supported by reservoir-engineering literature;
- assumptions that remain to be frozen or validated during implementation.

AURORA uses OPM Flow as a full-physics/high-fidelity reference simulator, not literal real-world ground truth.

## 2. Validation scale

- **VALIDATED** — directly supported by the benchmark, OPM evidence, or established literature.
- **VALID WITH LIMITATION** — defensible for AURORA if the stated limitation is preserved.
- **IMPLEMENTATION VALIDATION REQUIRED** — engineering idea is defensible, but exact parameter/interface must still be tested.
- **REJECT / REDESIGN** — physically indefensible in the proposed form.

No REJECT / REDESIGN item was identified.

## 3. Egg benchmark assumptions

| Assumption | Decision | Basis / limitation |
|---|---|---|
| Egg is appropriate as a controlled waterflood benchmark | VALIDATED | Jansen (2014) defines Egg as a synthetic channelized oil-reservoir ensemble under waterflooding, used for flooding optimization and history matching. |
| Eight injectors and four producers are legitimate benchmark topology | VALIDATED | Published Egg definition and F2 deck audit agree. |
| Geological uncertainty can be represented using Egg permeability realizations | VALIDATED WITH LIMITATION | Egg provides 101 realizations in the published ensemble; AURORA's downloaded set contains 100 PERM realization files plus the base/reference material. The uncertainty is deliberately limited and is not a complete representation of real-field uncertainty. |
| 60×60×7 / 25,200-cell geometry is standard Egg structure | VALIDATED | Published benchmark and F2 audit agree; F2 found 18,553 active cells. |
| Porosity 0.2 is consistent with standard Egg | VALIDATED | Published benchmark and audited deck agree. |
| Standard simulation horizon is 3,600 days | VALIDATED | Published benchmark and F2/F3 execution agree. |
| Producer BHP 395 bar is standard Egg operating condition | VALIDATED | Jansen reports 39.5×10^6 Pa = 395 bar; the audited deck contains raw 395 producer BHP. |
| 79.5 m³/day per injector is a standard Egg injection target | VALIDATED | Jansen reports 79.5 m³/day per well; F3 experimentally verified the baseline OPM output at 79.5 for each injector. |
| Raw WCONINJE value 420 is a BHP limit in the audited case | VALIDATED | OPM WCONINJE semantics include RATE and BHP-limit fields; the audited record is RATE 79.5, defaulted reservoir-rate field, then 420. Recent Egg studies also use an injector maximum pressure of 420 bar, although some Egg variants use 410 bar. AURORA must document the exact audited-deck convention rather than claim all Egg implementations use 420. |
| Egg is realistic enough to stand in for an actual oil field | REJECTED AS A CLAIM | Egg is synthetic and intentionally simplified. It is suitable for controlled counterfactual experiments, not proof of real-field performance. |

## 4. Physical model interpretation

The standard Egg model is a small, synthetic, channelized reservoir. Jansen's published parameters include 8 m × 8 m lateral grid blocks, 4 m thickness, porosity 0.2, slightly compressible oil/water, incompressible rock, zero capillary pressure, specified Corey-style relative permeability behaviour, initial top-layer pressure 40 MPa, producer BHP 39.5 MPa, and 3,600-day life.

These assumptions are legitimate for a benchmark experiment because they are part of the benchmark definition. They must not be generalized into claims that real reservoirs have the same properties.

AURORA should therefore describe Egg as a **controlled synthetic geological ensemble**, not as a realistic replica of a particular field.

## 5. Control-variable choice

### Injector-rate control

**VALIDATED.**

Using water-injection rate as the primary control variable is standard for Egg optimization studies and is directly supported by the supplied schedule. F3 additionally proved that AURORA can change an active injector-rate command and obtain a different OPM full-physics response.

The F3 perturbation from INJECT1 = 79.5 to 60.0 was a feasibility perturbation only. It is not evidence that 60.0 is an optimal operating rate.

### Producer controls

**VALIDATED WITH LIMITATION.**

Holding producers at the benchmark BHP while optimizing injection is consistent with the standard Egg setup. AURORA should not imply that producer controls are impossible or irrelevant in real reservoir management; they are simply outside the initial control scope.

### Action bounds

**IMPLEMENTATION VALIDATION REQUIRED.**

The standard benchmark supports an upper injection target of 79.5 m³/day per well. Literature variants commonly optimize injection within a bounded range such as 0–79.5 m³/day (some studies use a small positive lower bound).

AURORA should initially use benchmark-consistent bounds and explicitly document any nonzero lower bound. It must not invent a field-operational minimum and present it as an Egg fact.

## 6. Pressure constraints

Pressure is a physically meaningful safety/operational constraint for injection wells.

The audited Egg schedule contains an injector RATE target of 79.5 followed by a BHP-limit value of 420 under METRIC units. OPM's WCONINJE representation explicitly contains surface-rate, reservoir-rate and BHP-limit fields. Published Egg studies use injector maximum-BHP constraints, although values differ across variants (notably 410 and 420 bar).

Therefore:

- using injector BHP as a QP safety constraint is **VALIDATED as an engineering concept**;
- using **420 bar for this audited AURORA Egg case** is defensible if the exact deck semantics are retained and verified during implementation;
- AURORA must not claim that 420 bar is a universal physical fracture-pressure limit or a universal Egg value;
- a real-field pressure limit would require field-specific engineering information.

This distinction is important: a simulator control limit is not automatically a proven geomechanical fracture limit.

## 7. CRM / reduced-order model

### CRM as a fast waterflood model

**VALIDATED.**

CRM is an established reservoir-management model for waterflooding. The literature describes injection rates as input signals and production rates as reservoir responses, with producer BHP included where available. CRM estimates connectivity/gain and response time constants and has been used for rapid waterflood prediction and injection-allocation optimization.

This matches AURORA's need for a computationally cheap reduced-order model between expensive full-physics evaluations.

### CRMIP-style injector-producer representation

**VALIDATED WITH LIMITATION.**

An injector-producer-pair representation is defensible because CRMIP assigns connectivity and time-constant parameters to injector-producer pairs. This is especially useful for a multi-injector/multi-producer system such as Egg.

However, CRM remains a reduced-order approximation. It does not reproduce the complete multiphase spatial physics available in OPM.

### CRM on a channelized heterogeneous reservoir

**VALID WITH IMPORTANT LIMITATION.**

CRM literature warns that simpler producer-based CRM formulations can perform poorly when heterogeneity is strong. Egg is deliberately channelized and heterogeneous. AURORA should therefore prefer an injector-producer-pair formulation and must measure its prediction error against OPM rather than assume fidelity.

This limitation actually supports AURORA's planned mismatch-calibration architecture: the ROM is allowed to be imperfect, but the imperfection must be measured.

### Oil/water separation

**IMPLEMENTATION VALIDATION REQUIRED.**

Basic CRM predicts total production response. Literature supports coupling CRM with fractional-flow modelling to separate oil and water responses.

AURORA must explicitly state whether its ROM predicts liquid rate only, separately models oil/water, or adds a fractional-flow component. It must not silently treat a basic CRM liquid-rate prediction as an oil-rate prediction.

## 8. Partial observation and recurrent control

**VALID AS AN EXPERIMENTAL DESIGN CHOICE.**

Operational reservoir control does not require exposing the complete simulator grid state to the controller. Restricting the controller to well-level operational measurements/history while reserving OPM full state for evaluation is defensible and creates a meaningful partial-observation problem.

AURORA must freeze the controller-visible observation schema before final experiments and prevent privileged OPM grid-state information from leaking into the policy.

Using recurrence is a machine-learning design choice rather than a reservoir-engineering fact. F5 therefore does not claim that RecurrentPPO is superior; that is an empirical question for later experiments.

## 9. QP safety projection

**VALID AS A CONTROL ARCHITECTURE, WITH IMPLEMENTATION VALIDATION REQUIRED.**

A safety projection that modifies a proposed injector action to satisfy explicitly defined operational constraints is conceptually defensible.

The QP must operate on constraints that have engineering meaning, such as injection bounds and pressure limits. It cannot make an unsafe model safe merely by calling a mathematical inequality a reservoir constraint.

Accordingly:

1. each constraint must map to a physical or operational quantity;
2. its limit must be documented;
3. the ROM-to-constraint prediction must be validated against OPM;
4. QP infeasibility/slack must be logged;
5. realized OPM constraint outcomes must be evaluated after projection.

The final claim should be **constraint-aware or safety-filtered control in the defined experimental environment**, not unconditional real-world safety.

## 10. ROM–OPM mismatch

**STRONGLY VALIDATED AS A NECESSARY DESIGN PRINCIPLE.**

Because CRM is deliberately lower fidelity than OPM and Egg is heterogeneous, treating CRM predictions as exact would be indefensible.

AURORA's plan to compute residuals between ROM predictions and OPM outcomes is therefore physically and scientifically appropriate.

The system should preserve:

`same state/history + candidate action → ROM prediction`

and

`same experimental condition + executed action → OPM response`

then calculate the mismatch using consistently defined quantities and horizons.

The residual must not mix incompatible quantities, units, timestamps or aggregation levels.

## 11. One-sided mismatch calibration

**VALID AS AN UNCERTAINTY-MANAGEMENT METHOD; EMPIRICAL VALIDATION REQUIRED.**

Using a one-sided calibrated margin around a safety-relevant prediction is appropriate when the engineering concern is directional, for example underpredicting pressure.

F5 does not establish that a particular conformal/calibration method will achieve the desired coverage on Egg. That must be tested using calibration data separated from final-test geology.

The margin should be interpreted as an empirically calibrated protection against observed ROM/full-physics mismatch within the experimental distribution, not a universal guarantee of reservoir safety.

## 12. Geological train/calibration/test separation

**VALIDATED AND REQUIRED.**

The Egg ensemble exists specifically to represent geological uncertainty. Using distinct realizations for training/tuning, mismatch calibration, and final evaluation is scientifically defensible.

The split must be frozen before final experiments. Final-test realizations must not influence:

- RL training;
- CRM tuning choices;
- QP/margin tuning;
- conformal calibration;
- hyperparameter selection;
- iterative design decisions.

The exact split ratio is an experimental-design decision and should be chosen before implementation-scale experimentation rather than retrofitted after seeing results.

## 13. Economic objective

**VALID WITH LIMITATION.**

NPV-style objectives are common in Egg optimization literature, but published studies use different economic coefficients. Therefore no single oil price, water-production cost, water-injection cost or discount rate should be presented as a physical property of Egg.

AURORA may use a documented economic scenario for reward/evaluation, but it should:

- distinguish physical benchmark parameters from assumed economic parameters;
- report the coefficients;
- use consistent units;
- perform sensitivity analysis if economic conclusions depend strongly on them.

Physical performance metrics should remain available alongside economic metrics.

## 14. Held-out OPM evaluation

**VALIDATED AS THE PRIMARY CONTROLLED COUNTERFACTUAL TEST.**

Historical field data cannot reveal what would have happened under actions that were never taken. OPM/Egg can because the simulator can be rerun under alternative actions while controlling the geological realization.

F3 experimentally demonstrated this capability.

Therefore Egg/OPM is the correct place to make controlled comparative claims such as controller A versus controller B under the same realization and experimental conditions.

This does not turn OPM into real-world ground truth.

## 15. Volve role

**VALID ONLY AS REAL-FIELD GROUNDING, NOT COUNTERFACTUAL PROOF.**

AURORA may later use Volve data to demonstrate that the variables, time-series structure, CRM fitting problem and operational context have real-field relevance.

It must not claim from historical Volve data alone that AURORA would have outperformed the actions actually taken, because the counterfactual outcomes are unobserved.

F7 will validate the exact Volve role and accessible variables.

## 16. HIL / ESP32 interpretation

**VALID WITH LIMITATION.**

The ESP32-S3 layer is defensible as a hardware-in-the-loop deployment analogue for:

- communication;
- serialization;
- command acknowledgement;
- watchdogs;
- interlocks;
- manual override;
- fault injection;
- timing/latency;
- safe failure behaviour.

It is not a physical reservoir model and does not make the simulated reservoir more geologically realistic.

The hardware should therefore be described as **deployment/control-system validation**, not as the source of AURORA's reservoir-engineering novelty.

## 17. Key domain risks carried into implementation

| Risk | Why it matters | Required treatment |
|---|---|---|
| CRM underfits channelized Egg dynamics | Bad ROM predictions could mislead controller/QP | Measure against OPM; use CRMIP-style structure; calibrate mismatch |
| Pressure signal not yet conveniently extracted | QP cannot enforce pressure constraint without a numerical signal | Implement and test OPM pressure/BHP extraction |
| 420-bar limit misinterpreted | Simulator BHP constraint could be falsely described as fracture pressure | Call it the audited-case injector BHP limit unless independent geomechanical evidence exists |
| Oil/water handling in CRM unclear | Basic CRM liquid response is not automatically oil response | Freeze liquid vs fractional-flow/oil-water ROM design |
| Economic coefficients arbitrary | Could make controller comparison depend on hidden assumptions | Publish coefficients + physical metrics + sensitivity analysis |
| Privileged simulator state leaks into policy | Invalidates partial-observation claim | Explicit observation contract and automated leakage checks |
| Geological test leakage | Inflates apparent generalization | Freeze realization split and hashes before experiments |
| QP labelled “safe” without realized verification | Mathematical feasibility does not prove reservoir constraint satisfaction | Evaluate projected actions in OPM and report violations/interventions |
| Overclaiming simulator evidence | Synthetic success ≠ field deployment proof | Keep Egg/OPM, Volve and HIL claims explicitly separated |

## 18. Assumptions register

### Validated now

- Egg is an appropriate synthetic waterflood benchmark.
- Eight injectors / four producers are correct.
- 3,600-day standard horizon is correct.
- 79.5 m³/day is the standard injector target.
- 395 bar is the standard producer BHP.
- Injection rate is a legitimate Egg control variable.
- The audited WCONINJE 420 value is interpretable as the injector BHP limit for this case.
- CRM is an established fast model for waterflood response/optimization.
- Injector-producer CRM is appropriate to investigate.
- ROM predictions must be validated against OPM.
- Held-out geological evaluation is appropriate.
- OPM is suitable for controlled counterfactual comparison.

### Must be frozen/tested during implementation

- exact numerical pressure/BHP extraction interface;
- final injector lower/upper action bounds;
- whether 420 bar remains the chosen safety constraint in all experiments;
- CRMIP parameterization and fitting procedure;
- oil/water separation or fractional-flow treatment;
- controller-visible observation vector;
- decision interval;
- QP constraint linearization/prediction formulation;
- slack policy;
- mismatch residual definition/horizon;
- calibration method and target coverage;
- OOD method;
- geological split;
- economic coefficients and reward weights.

None of these currently requires architectural redesign.

## 19. Concern #11 decision

Concern #11 asks whether the team understands the reservoir engineering deeply enough to avoid building a physically meaningless control experiment.

**Decision: CONDITIONAL PASS.**

The core reservoir/control architecture is defensible and is supported by the Egg benchmark, established CRM literature and F2/F3 empirical evidence.

However, domain validation cannot honestly be marked completely finished until the implementation freezes and tests the pressure extraction/constraint interpretation, CRM oil-water formulation, exact action bounds and other engineering parameters listed above.

Therefore Concern #11 should remain **yellow**, but it is now a **controlled yellow with explicit closure criteria**, not an unknown risk.

## 20. F5 Decision

# CONDITIONAL PASS

No reservoir-engineering assumption was found that requires abandoning or fundamentally redesigning AURORA.

The major architectural choices are defensible:

`controlled Egg waterflood → injection-rate decisions → fast CRM/CRMIP-style ROM → partial-observation controller → constraint-aware QP projection → OPM verification → measured ROM/full-physics mismatch → calibrated margin → held-out geological evaluation`

The remaining conditions are implementation-level domain checks, especially pressure extraction/limits, CRM liquid-versus-oil/water treatment, action bounds and experimental assumptions.

F5 therefore permits the feasibility process to advance to **F6 — State-of-the-Art, Gap & Novelty Verification**, while Concern #11 remains yellow until those closure criteria are satisfied.

## 21. External sources used

1. Jansen, J.D. (2014), *The Egg Model — a geological ensemble for reservoir simulation*, Geoscience Data Journal. DOI: 10.1002/gdj3.21.
2. Holanda, R.W., Gildin, E., Jensen, J.L. (2018), *A generalized framework for Capacitance Resistance Models and a comparison with streamline allocation factors*, Journal of Petroleum Science and Engineering, 162, 260–282.
3. Sayarpour, M., Zuluaga, E., Kabir, C.S., Lake, L.W. (2009), *The use of capacitance–resistance models for rapid estimation of waterflood performance and optimization*, Journal of Petroleum Science and Engineering, 69, 227–238.
4. Soroush et al. (2018), *A State-of-the-Art Literature Review on Capacitance Resistance Models for Reservoir Characterization and Performance Forecasting*, Energies, 11, 3368.
5. Open Porous Media initiative, *OPM Flow Reference Manual* and OPM WCONINJE parser/reference documentation.
6. Recent Egg optimization literature was used only to corroborate variant-specific injector BHP constraints and to distinguish 410-bar and 420-bar variants from the invariant benchmark facts.
