# F4 — AURORA Input–Output & Data Sufficiency Traceability Matrix

## Verdict: PASS

F4 tests whether the frozen AURORA architecture requires information that cannot be obtained or defensibly derived from Egg/OPM. DIRECT means already available; DERIVED means calculable from available information; IMPLEMENTATION means upstream information exists but software must expose/transform it; GAP means no defensible source exists.

| Requirement | AURORA use | Source / derivation | Status |
|---|---|---|---|
| Grid dimensions/geometry | Physical domain | Egg DIMENS/SPECGRID/DX/DY/DZ/TOPS | DIRECT |
| Active cells | Reservoir domain | Egg ACTNUM/ACTIVE.INC | DIRECT |
| Porosity | Reservoir/ROM | Egg PORO | DIRECT |
| Permeability X/Y/Z | Flow/geology | Egg PERMX; deck-defined Y/Z | DIRECT |
| NTG | Reservoir definition | Egg NTG | DIRECT |
| Fluid/PVT | Full physics | Egg PVCDO/PVTW | DIRECT |
| Rock properties | Full physics | Egg ROCK | DIRECT |
| Relative permeability | Water/oil displacement | Egg SWOF | DIRECT |
| Initialization | Initial state | Egg EQUIL/deck | DIRECT |
| Geological realizations | Uncertainty/generalization | PERM1–PERM100 | DIRECT |
| Train/calibration/test identity | Leakage-safe evaluation | Frozen split of realization IDs | DERIVED |
| Well identities/roles | Topology | Egg WELSPECS | DIRECT |
| Well locations/completions | Topology | Egg coordinates/COMPDAT | DIRECT |
| Injector controls | Controller actions | Egg WCONINJE | DIRECT |
| Producer controls | Operating conditions | Egg WCONPROD | DIRECT |
| Sequential timing | Control horizon | Egg schedule/TSTEP | DIRECT |
| Field oil/water/injection rates | Observation/evaluation | OPM FOPR/FWPR/FWIR | DIRECT |
| Field cumulative quantities | Evaluation | OPM FOPT/FWPT/FWIT | DIRECT |
| Producer oil/water/liquid rates | Observation/CRM/evaluation | OPM WOPR/WWPR/WLPR | DIRECT |
| Individual injector rates | Control verification/CRM | OPM WWIR | DIRECT |
| Reservoir pressure | Safety/state/reference | OPM UNRST PRESSURE | IMPLEMENTATION |
| Water saturation | Full-state reference | OPM UNRST SWAT | IMPLEMENTATION |
| Convenient BHP/pressure signal | Observation/constraints if selected | Request suitable OPM output/extract state | IMPLEMENTATION |
| Historical action sequence | Sequential context | Executed injector controls | DIRECT |
| Historical response sequence | Sequential context | OPM trajectories | DIRECT |
| Partial-observation vector | PPO/R-PPO input | Selected available operational signals/history | DERIVED |
| Observation history | Recurrent context | Software buffer | IMPLEMENTATION |
| RL action vector | Proposed injector decisions | Policy output mapped to controllable injectors | DERIVED |
| Action bounds | Valid/safe actions | Engineering configuration | IMPLEMENTATION; validate F5 |
| Action-to-OPM mapping | Execute decisions | Schedule/control update | IMPLEMENTATION; F3 proves feasibility |
| CRM inputs | ROM fitting | Injection + producer histories | DIRECT |
| CRM parameters/state | Fast model | Estimated from histories | DERIVED |
| CRM predictions | Control/safety prediction | Fitted ROM | DERIVED |
| Full-physics reference response | Validation/calibration | OPM | DIRECT |
| PPO/R-PPO action | Candidate decision | Policy(observation/history) | DERIVED |
| Recurrent hidden state | Partial-observation memory | RecurrentPPO internal state | IMPLEMENTATION |
| Reward | Learning/evaluation | Oil/water/injection/constraint terms | DERIVED |
| Economic coefficients | Economic reward if used | Documented experiment assumptions | IMPLEMENTATION |
| Constraint quantities/limits | QP safety | Signals + validated engineering limits | IMPLEMENTATION; validate F5 |
| QP matrices/vectors | Safety projection | ROM/local constraint representation | DERIVED |
| QP safe action | Executed action | CVXPY/OSQP solution | DERIVED |
| Intervention magnitude | Safety analysis | proposed minus projected action | DERIVED |
| Violation magnitude | Safety metric | realized quantity vs limit | DERIVED |
| Slack use | Feasibility diagnostic | QP solution | DERIVED |
| ROM prediction | Mismatch measurement | CRM/ROM | DERIVED |
| OPM same-action outcome | Mismatch reference | Counterfactual OPM execution | DIRECT |
| ROM–OPM residual | Model error | OPM outcome minus ROM prediction | DERIVED |
| Calibration residual set | UQ | Calibration-only residuals | DERIVED |
| One-sided calibrated margin | Mismatch-aware safety | Statistical/conformal calibration | DERIVED |
| Coverage/error statistics | UQ validation | calibration/test outcomes | DERIVED |
| OOD indicator | Detect unsupported operation | selected features/residual statistics | IMPLEMENTATION |
| Fixed schedule baseline | Comparator | Existing Egg schedule | DIRECT |
| Heuristic baseline | Comparator | Rule-based controller | DERIVED |
| Conventional optimization/QP/MPC | Comparator | ROM + constraints | IMPLEMENTATION |
| PPO comparator | Learning comparator | Gym interface | IMPLEMENTATION |
| RecurrentPPO | Principal controller | Gym + recurrent state | IMPLEMENTATION |
| Safety-filtered controller | Main safety evaluation | policy + QP | IMPLEMENTATION |
| Held-out geological results | Generalization | frozen final-test realizations + OPM | DERIVED |
| Performance/safety metrics | Scientific comparison | OPM/controller trajectories | DERIVED |
| Runtime metrics | Practical comparison | experiment logging | DERIVED |
| Statistical comparison | Research evaluation | per-realization/per-seed results | DERIVED |
| Random seeds/config/version | Reproducibility | experiment metadata/Git | IMPLEMENTATION |
| Realization ID | Reproducibility | Egg filename/manifest | DIRECT |
| OPM version/image digest | Reproducibility | F3 environment manifest | DIRECT |
| Input hashes | Provenance | SHA-256 manifests | DERIVED |
| Dashboard telemetry | Demo/monitoring | observations/actions/outcomes/constraints | DERIVED |
| Proposed vs safe action display | Explain QP | policy + QP outputs | DERIVED |
| ESP32 command | HIL | serialize safe action | DERIVED |
| ESP32 status/watchdog/interlock | HIL/fault handling | firmware | IMPLEMENTATION |
| Manual override | HIL safety | firmware/interface | IMPLEMENTATION |
| Fault-injection event | HIL testing | test harness/firmware | IMPLEMENTATION |
| End-to-end episode log | Audit/replay | aggregate pipeline telemetry | DERIVED |

## Evidence and broken-arrow analysis

F2 established the reservoir definition required by the full-physics model: geometry, active cells, porosity, permeability, fluid/rock properties, relative permeability, equilibrium initialization, wells, completions, producer/injector controls, and the geological ensemble. It identified eight injectors, four producers, and 100 permeability realizations.

F3 established the operational information path. OPM Flow executed the Egg case through all 120 report steps / 3,600 days and produced machine-readable outputs. Field and well trajectories were extracted. INJECT1 was then changed from 79.5 to 60.0 while INJECT2–INJECT8 remained unchanged. OPM realized the requested change, total field injection changed from 636.0 to 616.5, and field/producer trajectories and cumulative outcomes changed measurably.

The frozen information chain is:

`Egg → OPM → observations → CRM/ROM → Gymnasium → PPO/RecurrentPPO → proposed action → QP → safe action → OPM → response → mismatch → calibration → held-out evaluation → statistics → dashboard/HIL`

No arrow currently terminates in a source-less information dependency.

Items not already available as ready-to-consume variables are either extraction work (for example convenient numerical PRESSURE/SWAT access), internal model/software quantities (CRM parameters, recurrent state, QP matrices, residuals, calibrated margins), or engineering design parameters requiring F5 validation (limits, action bounds, economic assumptions).

## Conditions carried forward

**Pressure/state extraction:** F3 established PRESSURE and SWAT presence in OPM restart output. Numerical extraction must be implemented and validated before these signals are relied upon operationally.

**Safety limits/action bounds:** availability of signals does not establish defensible engineering limits. F5 must validate these assumptions.

**Economics:** physical oil/water/injection quantities exist. Any prices, costs, discounting or reward weights are documented experimental assumptions, not Egg measurements.

**Partial observability:** the interface contract must separate controller-visible observations from privileged OPM full state used for calibration/evaluation.

**Geological leakage:** the realization split must be frozen before final experimentation. Final-test geology must not influence training, calibration, tuning or iterative design.

**Reference interpretation:** OPM is AURORA's full-physics/high-fidelity reference simulator, not literal real-world ground truth.

## Concern #4 decision

Concern #4 asks whether available inputs contain enough information to support the outputs and information flows required by AURORA.

**YES — PASS at feasibility level.**

No fatal information gap was identified. Required physical information is directly available or derivable; intelligent-controller/safety quantities are generated internally from available upstream signals; and the remaining engineering assumptions are explicitly assigned to F5 validation.

Concern #4 can therefore move from **yellow to green**.

This does not mean every interface is implemented. It means no current evidence indicates that implementation will fail because a required information source does not exist.

## Final F4 Decision

# PASS

The frozen AURORA architecture is informationally feasible. No GAP item requiring redesign or abandonment was identified.

Principal work carried forward: implement restart-state extraction and use F5 to validate reservoir-engineering assumptions, operational constraints, action bounds and physical interpretations.

**Next: F5 — Reservoir Engineering Assumptions & Domain Validation Report.**
