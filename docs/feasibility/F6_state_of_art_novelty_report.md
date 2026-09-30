# F6 — State-of-the-Art, Gap & Novelty Verification Report
## FINAL DEEP-SWEEP VERSION — replaces the earlier F6 draft

## Verdict

# CONDITIONAL PASS

A defensible research gap survives an adversarial, multi-axis literature search, but only under a narrow integration-and-evaluation claim. Broad novelty claims are rejected.

---

## 1. Purpose

F6 asks four questions:

1. Has the central AURORA idea already been done?
2. Which individual components are established prior art?
3. What exact gap remains defensible after aggressive searching?
4. What experiments would make that gap scientifically meaningful rather than merely an assembly of known components?

The search strategy was intentionally adversarial: it attempted to find papers capable of invalidating AURORA's novelty.

---

## 2. Final novelty boundary in one sentence

The strongest surviving AURORA contribution is:

> **An experimentally evaluated mismatch-aware supervisory architecture for partially observed sequential waterflood control that couples recurrent reinforcement learning to a CRM/CRMIP-style physical reduced-order model, explicitly measures that model's error against a full-physics reservoir simulator, converts safety-relevant error into a separately calibrated one-sided margin used by an explicit action-projection layer, and tests the resulting safety/performance trade-off on untouched geological realizations in full physics.**

This is a candidate contribution, not a claim of guaranteed originality or superiority.

---

## 3. What is definitively NOT novel

The deep sweep found established work for every item below. AURORA must not claim invention of:

- RL for waterflood optimization;
- RL on the Egg reservoir;
- deep RL under geological uncertainty;
- safe/constrained RL for waterflood production optimization;
- partial-observation reservoir RL;
- Dec-POMDP formulations for reservoir control;
- recurrent/LSTM temporal reservoir models;
- surrogate-assisted RL for waterflood control;
- high-fidelity simulator re-evaluation of surrogate-optimized controls;
- CRM/CRMIP for waterflood prediction;
- CRM/CRMIP for injection-rate optimization;
- CRM state-space/control formulations;
- CRM uncertainty/probabilistic forecasting;
- CRM structural/model-error modelling;
- CRM coupled to nonlinear constrained production optimization;
- robust waterflood optimization under geological uncertainty;
- learned feasibility/constraint models for Egg/reservoir optimization;
- QP/action projection/shielding as a general safe-control mechanism;
- conformal prediction;
- conformal uncertainty quantification of surrogate models;
- conformal prediction for hydrocarbon production forecasting;
- recurrent policies as a generic response to partial observability;
- HIL, watchdogs, interlocks or embedded fault handling.

The novelty must therefore arise from the specific scientific integration, use of measured model discrepancy inside the safety mechanism, and leakage-safe evaluation.

---

## 4. Closest and highest-priority prior art

### Tier A — must-read / closest threats

#### A1. Chen et al. (2025), Worst-Case Soft Actor-Critic-Based Safe Reinforcement Learning Method for Nonlinear Constrained Waterflood Reservoir Production Optimization
SPE Journal, 30(12), 7745–7766. DOI: 10.2118/230322-PA.

Why it matters:
- safe RL is already applied directly to constrained waterflood production optimization;
- uses a constrained MDP;
- uses a safety critic and CVaR/worst-case logic;
- balances economic reward and constraints.

Impact on AURORA:
- destroys any “first safe RL for waterflood” claim;
- should be a conceptual comparator/discussion anchor;
- AURORA must distinguish explicit external projection + physical ROM discrepancy calibration from learned safety-critic/CVaR constraint handling.

#### A2. Mamghaderi, Aminshahidy & Bazargan (2021), Prediction of waterflood performance using a modified capacitance-resistance model: A proxy with a time-correlated model error
Journal of Petroleum Science and Engineering, 198, 108152. DOI: 10.1016/j.petrol.2020.108152.

Why it matters:
- explicitly models intrinsic CRM structural discrepancy;
- embeds stochastic and non-stochastic time-correlated model error;
- generates probabilistic output ranges.

Impact:
- CRM discrepancy/error modelling is not novel;
- AURORA's distinction must be the use of separately measured CRM/full-physics error to calibrate an operational safety margin for action projection.

#### A3. Mamghaderi, Aminshahidy & Bazargan (2020), Error behavior modeling in Capacitance-Resistance Model
Journal of Natural Gas Science and Engineering, 77, 103228. DOI: 10.1016/j.jngse.2020.103228.

Why:
- directly addresses inherent CRM uncertainty/model error;
- couples CRM error dynamics with EnKF.

Impact:
- further prevents AURORA from claiming discovery of CRM model-form uncertainty.

#### A4. Sayarpour, Zuluaga, Kabir & Lake (2009), The use of capacitance–resistance models for rapid estimation of waterflood performance and optimization
Journal of Petroleum Science and Engineering, 69, 227–238. DOI: 10.1016/j.petrol.2009.09.006.

Why:
- foundational CRM waterflood optimization;
- injection rates as inputs and production rates as outputs;
- CRMT/CRMP/CRMIP;
- numerical-flow-simulation verification;
- water reallocation optimization.

Impact:
- CRM + waterflood optimization + simulator comparison is old prior art.

#### A5. Holanda, Gildin & Jensen (2018), A generalized framework for Capacitance Resistance Models and a comparison with streamline allocation factors
Journal of Petroleum Science and Engineering, 162, 260–282. DOI: 10.1016/j.petrol.2017.10.020.

Why:
- state-space CRM representations;
- explicitly enables linear control algorithms;
- optimization-friendly matrix formulation.

Impact:
- “CRM as control-oriented state-space model” is not novel.

#### A6. Scalable and adaptive injection-production control in reservoirs via a multi-agent reinforcement learning approach (2025)
Energy Reports. DOI: 10.1016/j.egyr.2025.108983.

Why:
- reservoir injection-production RL;
- surrogate-assisted;
- partial local observations;
- explicitly formulated as a Dec-POMDP;
- graph-conditioned multi-agent control;
- high relevance to AURORA's partial-observation motivation.

Impact:
- “partial observation + reservoir RL + surrogate” is not novel.

#### A7. Spatiotemporal graph-based surrogate modeling and deep reinforcement learning for multi-layer injection-production decision in waterflood reservoirs (2026)
Engineering Applications of Artificial Intelligence, 181, 115452. DOI: 10.1016/j.engappai.2026.115452.

Why:
- GCN-Transformer-LSTM surrogate;
- TD3 control;
- waterflood injection-production optimization;
- surrogate predictions re-evaluated in a high-fidelity simulator;
- reports surrogate/full-simulator errors and speedup.

Impact:
- “temporal surrogate + DRL + simulator re-evaluation” is not novel;
- simply measuring surrogate accuracy is insufficient differentiation.

#### A8. Surrogate-Assisted Optimization of Highly Constrained Oil Recovery Processes Using Classification-Based Constraint Modeling (2025)

Why:
- constrained oil-recovery optimization;
- Egg and UNISIM benchmark reservoirs;
- surrogate objective model plus learned feasible/infeasible constraint classifier.

Impact:
- Egg + surrogate + learned constraint handling is occupied prior art.

#### A9. ORACLE: Online reinforcement-driven adaptive constraint learning engine for nonlinear optimization (Aghayev et al., 2026), AIChE Journal

Why:
- reinforcement-driven adaptive constraint/feasibility learning;
- Egg reservoir benchmark;
- surrogate objective and constraint modelling;
- public implementation.

Impact:
- highly relevant adjacent constraint-learning work;
- should be inspected carefully during implementation and final paper writing.

#### A10. Gopakumar et al. (2026), Uncertainty quantification of surrogate models using conformal prediction
Machine Learning: Science and Technology, 7, 015025. DOI: 10.1088/2632-2153/ae2e7b.

Why:
- conformal prediction applied directly to surrogate-model UQ;
- contemporary evidence that “conformalize surrogate error” is itself established.

Impact:
- AURORA cannot claim conformal surrogate UQ as its invention.

#### A11. Idris et al. (2025), Out-of-Sample Hydrocarbon Production Forecasting ... with Inductive Conformal Prediction
arXiv:2508.14078.

Why:
- petroleum/hydrocarbon forecasting;
- Volve and Norne data;
- LSTM/BiLSTM/GRU/XGBoost;
- inductive conformal prediction for prediction intervals.

Impact:
- petroleum + recurrent forecasting + conformal UQ is already present.

#### A12. Improved CRM Model for Inter-Well Connectivity Estimation and Production Optimization: Case Study for Karst Reservoirs (2019), Energies 12(5), 816

Why:
- injector-producer CRM;
- production optimization;
- injection rate as control;
- NPV objective;
- hybrid nonlinear constraints.

Impact:
- CRM + optimization + constraints is not novel.

---

## 5. Important waterflood/RL literature

### Hourfar et al. (2019)
*A reinforcement learning approach for waterflooding optimization in petroleum reservoirs.*
Engineering Applications of Artificial Intelligence, 77, 98–116.
DOI: 10.1016/j.engappai.2018.09.019.

Establishes RL-based waterflood management and Egg-based experiments.

### Ma et al. (2019)
*Waterflooding Optimization under Geological Uncertainties by Using Deep Reinforcement Learning Algorithms.*
SPE-196190-MS.
DOI: 10.2118/196190-MS.

Establishes deep RL waterflood optimization under geological uncertainty.

### Miftakhov, Efremov & Al-Qasim (2020)
*Reinforcement Learning From Pixels: Waterflooding Optimization.*
OMAE2020-18574.
DOI: 10.1115/OMAE2020-18574.

Uses rich pressure/saturation representations for RL waterflood control.

### Zhang et al. (2022)
*Training effective deep reinforcement learning agents for real-time life-cycle production optimization.*
Journal of Petroleum Science and Engineering, 208, 109766.
DOI: 10.1016/j.petrol.2021.109766.

Establishes DRL for sequential real-time life-cycle production control.

### Multi agent physics informed reinforcement learning for waterflooding optimization (2025)

Uses physics-informed multi-agent RL and the Egg model.

### Scalable/adaptive MARL injection-production control (2025)

Particularly relevant because it formalizes reservoir control as a Dec-POMDP with local observations and integrates an online-updated surrogate.

---

## 6. Important CRM / reduced-order literature

### Sayarpour et al. (2009)
Foundational fast CRM waterflood prediction and injection optimization.

### Sayarpour, Kabir, Sepehrnoori & Lake (2011)
*Probabilistic history matching with the capacitance–resistance model in waterfloods: A precursor to numerical modeling.*
JPSE 78(1), 96–108.
DOI: 10.1016/j.petrol.2011.05.005.

Important because:
- CRM uncertainty/probabilistic history matching already exists;
- compares CRM uncertainty results with finite-difference simulations;
- demonstrates CRM as a precursor to numerical modelling.

### Holanda et al. (2018)
State-space/control-friendly CRM formulation.

### Mamghaderi et al. (2020, 2021)
Explicit CRM structural/model-error modelling.

### Improved CRM/Karst optimization (2019)
CRM-Koval / injector-producer formulation used for constrained NPV optimization.

These papers collectively mean AURORA's CRM contribution cannot be “fast physical proxy,” “optimization,” “uncertainty,” “model error,” or “control formulation” individually.

---

## 7. Important surrogate/optimization literature

### Production optimization under waterflooding with LSTM and metaheuristic algorithm (2021/2022)
Uses LSTM reservoir proxies and particle swarm optimization; reports blind validation and simulator agreement.

### Active-learning surrogate ensemble multi-objective waterflood optimization (2025)
Uses active learning and surrogate ensembles for multi-objective waterflood production optimization.

### Robust optimisation of water flooding using an experimental-design surrogate (2020)
Explicitly handles geological uncertainty using surrogate-based robust optimization.

### Spatiotemporal graph surrogate + TD3 (2026)
Very close modern neighbor: temporal/spatial surrogate + DRL + high-fidelity simulator re-evaluation.

Therefore “surrogate-assisted optimization under geology” is established.

---

## 8. Important uncertainty/calibration literature

AURORA's UQ story must distinguish several existing families:

1. CRM probabilistic history matching.
2. CRM time-correlated structural-error modelling.
3. robust optimization over geological uncertainty.
4. surrogate ensembles / active learning.
5. conformal prediction for generic surrogate UQ.
6. conformal prediction for hydrocarbon time-series forecasting.
7. sequential/time-series conformal methods generally.

The research question is therefore not “can we quantify uncertainty?”

It is:

> Can a safety-relevant, directionally defined residual between a physical reduced-order waterflood model and a full-physics reference be calibrated on separate geology and used to modify the explicit action projection in a way that improves realized held-out constraint behavior?

---

## 9. Partial observability finding

The deep sweep materially changed F6.

Partial observability is **not** an unoccupied reservoir-control gap.

The 2025 scalable/adaptive injection-production MARL paper explicitly describes a Dec-POMDP with local observations and centralized-training/decentralized-execution concepts.

Therefore AURORA must not claim:
- first POMDP reservoir controller;
- first partially observed reservoir RL;
- first local-observation reservoir RL.

AURORA may still test a distinct architecture:
- single supervisory recurrent controller;
- deliberately restricted operational observation vector;
- recurrent PPO vs feed-forward PPO;
- physical CRM safety model;
- separately calibrated mismatch margin.

Recurrence remains an experimental mechanism, not a novelty claim.

---

## 10. Constraint/safety finding

Safe waterflood RL already exists through WCSAC/CMDP/CVaR.

Constraint-learning and surrogate-feasibility approaches also exist for Egg/oil-recovery optimization.

Therefore AURORA's safety contribution must be described structurally:

`learned controller proposal`
→ `physical ROM predicts safety-relevant response`
→ `explicit projection solves constrained correction`
→ `ROM prediction is inflated by separately calibrated one-sided discrepancy margin`
→ `projected action is evaluated in full physics`.

The potentially distinctive element is **not constraint handling itself**, but the insertion of an empirically calibrated physical-model discrepancy margin into an explicit supervisory projection and the subsequent held-out full-physics test.

---

## 11. Search for the exact central combination

The deep sweep used combinations spanning:

- waterflood + RL + partial observation/POMDP;
- waterflood + recurrent RL/LSTM/GRU/PPO;
- reservoir + safe RL;
- waterflood + CMDP/CVaR;
- waterflood + action projection/shield/safety filter;
- petroleum + control barrier functions;
- waterflood + QP + RL;
- CRM + RL;
- CRM + optimization;
- CRM + constraints;
- CRM + model error/discrepancy;
- CRM + uncertainty/probabilistic forecasting;
- CRM + state-space/control;
- waterflood + surrogate + RL;
- waterflood + surrogate uncertainty;
- waterflood + geological uncertainty/robust optimization;
- petroleum/reservoir + conformal prediction;
- waterflood + conformal prediction;
- surrogate + conformal prediction;
- Egg + RL;
- Egg + constraints/feasibility;
- Egg + surrogate;
- 2025–2026 reservoir-control literature.

### Result

The search found prior art for nearly every pairwise and several three-way combinations.

It did **not identify a paper that clearly demonstrates the complete central AURORA mechanism**:

`partial operational observations`
+ `recurrent RL`
+ `CRM/CRMIP physical ROM`
+ `explicit action projection`
+ `ROM/full-physics residual measured directly`
+ `separate one-sided statistical calibration of safety-relevant residual`
+ `calibrated margin inserted into projection`
+ `calibration geology separated from final-test geology`
+ `realized safety/performance evaluated on held-out full-physics realizations`.

This absence is search-supported, not a proof of universal nonexistence.

---

## 12. Why the surviving gap is meaningful

The gap is only scientifically meaningful if AURORA tests a causal design question rather than assembling components.

The central comparison must be:

### A. Raw recurrent controller
No projection.

### B. Recurrent controller + nominal projection
Uses CRM prediction as if it were exact.

### C. Recurrent controller + mismatch-calibrated projection
Uses the same projection but tightens the safety condition using a one-sided margin learned only from calibration residuals.

If C reduces **realized OPM violations** relative to B without simply destroying production/economic performance, the mismatch-calibration mechanism has empirical value.

If C behaves no better than B, the hypothesis fails. That is still a valid scientific result.

---

## 13. Recommended primary research question

> **Can an explicit waterflood action-projection layer that accounts for a one-sided, statistically calibrated CRM/full-physics prediction discrepancy reduce realized operational-constraint violations on unseen geological realizations, relative to both an unfiltered recurrent controller and the same controller with a nominal uncalibrated projection, without an excessive loss of production/economic performance?**

This is stronger and more defensible than “Can AI optimize a reservoir?”

---

## 14. Recommended primary hypothesis

> **On held-out Egg geological realizations, a one-sided mismatch-calibrated projection will reduce the frequency and/or magnitude of realized OPM operational-constraint violations relative to both raw RecurrentPPO and RecurrentPPO with a nominal uncalibrated projection, while preserving more production/economic performance than a uniformly conservative safety margin not informed by measured mismatch.**

This remains a hypothesis until tested.

---

## 15. Required experiment ladder

At minimum:

1. fixed Egg schedule;
2. heuristic/rule-based controller;
3. conventional optimization/QP/MPC-style comparator where feasible;
4. PPO under frozen partial observations;
5. RecurrentPPO under identical observations;
6. RecurrentPPO + nominal QP projection;
7. RecurrentPPO + mismatch-calibrated QP projection;
8. conservative fixed-margin projection;
9. safe-RL comparator if feasible, preferably conceptually aligned with the 2025 WCSAC literature;
10. privileged/full-information oracle diagnostic where useful.

The most important ablation is **6 vs 7**.

Without it, AURORA cannot isolate the value of mismatch calibration.

---

## 16. Required metrics

### Reservoir/economic
- cumulative oil;
- cumulative water production;
- cumulative water injection;
- NPV/documented economic objective;
- return.

### Constraint/safety
- OPM-realized violation count;
- violation frequency;
- maximum violation;
- cumulative violation magnitude;
- violation duration where meaningful;
- intervention frequency;
- correction norm;
- QP slack/infeasibility.

### ROM fidelity
- signed CRM prediction residual;
- MAE/RMSE;
- residual by realization;
- residual by operating regime;
- underprediction tail for safety-relevant quantity.

### Calibration
- target one-sided coverage;
- empirical calibration coverage;
- held-out coverage;
- margin sharpness/magnitude;
- coverage conditional on geology/operating regime where sample size permits.

### Generalization
- per-realization distributions;
- untouched final-test geology;
- multiple policy seeds;
- confidence intervals / bootstrap summaries.

### Computation
- CRM step time;
- policy inference time;
- QP solve time;
- OPM reference runtime;
- speed ratio.

---

## 17. Geological split requirement

The Egg realization ensemble should have functionally distinct groups:

- development/training;
- mismatch calibration;
- final held-out test.

The final-test group must not influence:
- RL training;
- CRM architecture/tuning decisions;
- QP tuning;
- margin calibration;
- hyperparameters;
- reward redesign;
- observation redesign;
- stopping decisions.

AURORA's claim becomes substantially weaker if “held-out” geology is repeatedly inspected during development.

---

## 18. One-sided calibration requirement

AURORA should calibrate the error in the direction relevant to violating the selected constraint.

For an upper pressure constraint, the dangerous error is typically **ROM underprediction of the realized full-physics pressure quantity**, not symmetric absolute error alone.

Therefore the residual sign convention must be frozen before experiments.

The report should provide:
- residual definition;
- calibration quantile/method;
- target coverage;
- empirical calibration coverage;
- untouched-test coverage;
- margin magnitude.

Do not call the result a universal safety guarantee.

---

## 19. CRM design implications from prior art

Prior literature creates several implementation requirements:

- use a CRMIP-style formulation where appropriate for injector-producer connectivity;
- do not assume CRM accurately represents strongly heterogeneous/channelized Egg dynamics;
- explicitly measure structural error;
- distinguish total-liquid prediction from oil/water phase prediction;
- consider a fractional-flow coupling if oil/water separation is required;
- preserve BHP effects where the chosen CRM formulation requires them;
- test identifiability and excitation of CRM parameters;
- avoid fitting/evaluating on identical trajectories.

AURORA's architecture is strengthened, not weakened, by treating CRM as intentionally imperfect.

---

## 20. Publication claim language

### Safe language

- “We investigate…”
- “We evaluate…”
- “Our literature review did not identify…”
- “To our knowledge, within the reviewed literature…”
- “The contribution is the integration and controlled evaluation of…”
- “We test whether…”
- “The proposed mismatch-aware projection…”

### Avoid unless later proven

- “first ever”
- “novel RL algorithm” if using standard PPO/R-PPO
- “first safe RL waterflood controller”
- “guaranteed safe”
- “real-world validated controller”
- “digital twin” unless true synchronized twin requirements are met
- “ground truth” for OPM
- “conformal prediction is our novelty”
- “CRM uncertainty is our novelty”

---

## 21. Demarcation from closest families

### Waterflood RL
AURORA adds no novelty merely by using RL.

### Partial-observation reservoir RL
Already exists. AURORA's recurrence/observation restriction is part of the evaluation architecture.

### Safe waterflood RL
Already exists. AURORA uses a different external mismatch-aware projection mechanism.

### Surrogate-assisted RL
Already exists. AURORA uses a physically interpretable CRM/CRMIP-style ROM and treats its discrepancy as an explicit safety-calibration variable.

### CRM optimization
Established for decades. AURORA does not claim it.

### CRM uncertainty/error modelling
Established. AURORA operationalizes separately measured discrepancy in a supervisory safety layer.

### Robust optimization under geology
Established. AURORA uses geology for development, calibration and untouched full-physics testing of the safety mechanism.

### Conformal surrogate UQ
Established generally. AURORA's potential contribution is its application to a safety-relevant physical-ROM/full-physics discrepancy inside sequential reservoir control, if successful.

---

## 22. HIL and Volve boundaries

### HIL
ESP32-S3 remains deployment/control-system validation:
- communication;
- latency;
- watchdogs;
- interlocks;
- manual override;
- fault injection;
- failure handling.

It is not the main research novelty.

### Volve
Volve can ground:
- real operational time series;
- CRM fitting plausibility;
- variable availability;
- practical reservoir context.

Historical Volve data cannot prove counterfactual superiority of AURORA's controller.

---

## 23. Remaining novelty threats

1. A paper not indexed or not surfaced by the search may duplicate the architecture.
2. 2025–2026 reservoir AI literature is moving quickly.
3. The integration may be viewed as obvious unless the calibrated-margin experiment shows a meaningful effect.
4. CRM may be too inaccurate for a useful sharp safety margin.
5. The selected constraint may be too easy and rarely activate.
6. A fixed conservative margin may perform as well as calibration.
7. Safe-RL baselines may dominate the proposed method.
8. Partial-observation recurrence may add no measurable benefit.
9. Geological calibration residuals may not transfer to final-test geology.
10. Poor split discipline could invalidate the strongest result.
11. If pressure extraction or prediction is weak, the chosen safety experiment may need another physically meaningful constraint.
12. Calling the mechanism “safe” too broadly could invite justified criticism.

---

## 24. F6 closure test

F6 is considered complete for capstone feasibility when all of the following are true:

- broad novelty claims have been explicitly rejected;
- closest prior art is recorded;
- a narrow search-supported gap is stated;
- a falsifiable research question exists;
- ablations isolate the claimed contribution;
- threats are documented;
- literature monitoring remains a continuing project task.

All six conditions are satisfied by this report.

---

## 25. Concern Table decisions

### #12 — Has somebody already done this?
**GREEN, with explicit qualification.**

Researchers have done most individual components and many close combinations. The deep sweep did not identify the complete central mismatch-calibrated projection architecture in petroleum waterflood control.

### #13 — What exactly is novel/different?
**GREEN, guarded.**

Candidate contribution:

`partial-observation recurrent controller`
+ `CRM/CRMIP physical ROM`
+ `explicit projection`
+ `measured ROM/full-physics safety residual`
+ `separate one-sided calibration`
+ `calibrated projection`
+ `untouched-geology full-physics evaluation`.

The contribution is the mechanism/integration/evaluation, not the components.

### #30 — Could it become publishable?
**GREEN as research feasibility only.**

The project now has a specific falsifiable question, strong neighboring literature, clear ablations and an identifiable scientific mechanism. This is not a prediction of acceptance or publication.

---

## 26. Final F6 Decision

# CONDITIONAL PASS — F6 CLOSED FOR FEASIBILITY

The deep adversarial search found substantial prior art and materially narrowed AURORA's proposed contribution.

It did **not** find evidence requiring abandonment of the project.

The final candidate research contribution is specifically the **use of separately calibrated, one-sided physical-ROM/full-physics discrepancy inside an explicit supervisory action-projection layer for partially observed sequential waterflood control, evaluated without geological leakage on held-out full-physics realizations**.

This wording should replace earlier broad descriptions of AURORA novelty.

F6 may now advance to F7 and G0.

F6 should only be reopened before publication/submission if:
- materially closer prior art is discovered;
- the implementation architecture changes substantially; or
- experiments show that the proposed distinguishing mechanism is not meaningful.

---

## 27. Highly relevant literature register

### Essential / closest
1. Chen et al. (2025). Worst-Case Soft Actor-Critic-Based Safe Reinforcement Learning Method for Nonlinear Constrained Waterflood Reservoir Production Optimization. *SPE Journal*, 30(12), 7745–7766. DOI 10.2118/230322-PA.
2. Mamghaderi, Aminshahidy & Bazargan (2021). Prediction of waterflood performance using a modified capacitance-resistance model: A proxy with a time-correlated model error. *JPSE*, 198, 108152. DOI 10.1016/j.petrol.2020.108152.
3. Mamghaderi, Aminshahidy & Bazargan (2020). Error behavior modeling in Capacitance-Resistance Model. *Journal of Natural Gas Science and Engineering*, 77, 103228. DOI 10.1016/j.jngse.2020.103228.
4. Sayarpour, Zuluaga, Kabir & Lake (2009). The use of capacitance–resistance models for rapid estimation of waterflood performance and optimization. *JPSE*, 69, 227–238. DOI 10.1016/j.petrol.2009.09.006.
5. Holanda, Gildin & Jensen (2018). A generalized framework for Capacitance Resistance Models and a comparison with streamline allocation factors. *JPSE*, 162, 260–282. DOI 10.1016/j.petrol.2017.10.020.
6. Scalable and adaptive injection-production control in reservoirs via a multi-agent reinforcement learning approach (2025). *Energy Reports*. DOI 10.1016/j.egyr.2025.108983.
7. Spatiotemporal graph-based surrogate modeling and deep reinforcement learning for multi-layer injection-production decision in waterflood reservoirs (2026). *Engineering Applications of Artificial Intelligence*, 181, 115452. DOI 10.1016/j.engappai.2026.115452.
8. Surrogate-Assisted Optimization of Highly Constrained Oil Recovery Processes Using Classification-Based Constraint Modeling (2025).
9. Aghayev et al. (2026). ORACLE: Online reinforcement-driven adaptive constraint learning engine for nonlinear optimization. *AIChE Journal*.
10. Gopakumar et al. (2026). Uncertainty quantification of surrogate models using conformal prediction. *Machine Learning: Science and Technology*, 7, 015025. DOI 10.1088/2632-2153/ae2e7b.

### Waterflood RL
11. Hourfar et al. (2019). A reinforcement learning approach for waterflooding optimization in petroleum reservoirs. *EAAI*, 77, 98–116. DOI 10.1016/j.engappai.2018.09.019.
12. Ma et al. (2019). Waterflooding Optimization under Geological Uncertainties by Using Deep Reinforcement Learning Algorithms. SPE-196190-MS. DOI 10.2118/196190-MS.
13. Miftakhov, Efremov & Al-Qasim (2020). Reinforcement Learning From Pixels: Waterflooding Optimization. OMAE2020-18574. DOI 10.1115/OMAE2020-18574.
14. Zhang et al. (2022). Training effective deep reinforcement learning agents for real-time life-cycle production optimization. *JPSE*, 208, 109766. DOI 10.1016/j.petrol.2021.109766.
15. Multi agent physics informed reinforcement learning for waterflooding optimization (2025).

### CRM / uncertainty / optimization
16. Sayarpour, Kabir, Sepehrnoori & Lake (2011). Probabilistic history matching with the capacitance–resistance model in waterfloods. *JPSE*, 78(1), 96–108. DOI 10.1016/j.petrol.2011.05.005.
17. Improved CRM Model for Inter-Well Connectivity Estimation and Production Optimization: Case Study for Karst Reservoirs (2019). *Energies*, 12(5), 816.
18. Soroush et al. (2018). A State-of-the-Art Literature Review on Capacitance Resistance Models for Reservoir Characterization and Performance Forecasting. *Energies*, 11, 3368.

### Surrogate / robust optimization
19. Production optimization under waterflooding with long short-term memory and metaheuristic algorithm (2021/2022).
20. Robust optimisation of water flooding using an experimental design-based surrogate model: A case study of a Niger-Delta oil reservoir (2020).
21. Active learning based surrogate ensemble assisted multi-objective optimization framework for reservoir water-flooding optimization (2025).
22. Robust waterflood optimization under geological uncertainties using streamline-based well pair efficiencies and assimilated models (2023).

### Conformal / uncertainty context
23. Idris et al. (2025). Out-of-Sample Hydrocarbon Production Forecasting: Time Series Machine Learning using Productivity Index-Driven Features and Inductive Conformal Prediction. arXiv:2508.14078.
24. Gopakumar et al. (2026). Uncertainty quantification of surrogate models using conformal prediction.
25. General conformal/time-series calibration literature should be cited for the statistical method; AURORA must not present conformal prediction itself as new.

### General safe-RL / POMDP context
26. Carr, Jansen, Junges & Topcu (2022). Safe Reinforcement Learning via Shielding under Partial Observability.
27. Contemporary POMDP continuous-control/recurrent-RL literature should support algorithmic choices, but is not part of the petroleum novelty claim.

---

## 28. Search record and interpretation

Searches covered direct phrases, synonyms and component intersections across:
- Google/web-indexed journal results;
- SPE/OnePetro-indexed results;
- Elsevier/ScienceDirect;
- Springer;
- Wiley;
- MDPI;
- IOP;
- arXiv/preprints;
- recent 2025–2026 work.

The search was expanded when a nearby concept was found, especially:
- safe RL;
- partial observability;
- surrogate re-evaluation;
- CRM discrepancy;
- constrained CRM optimization;
- conformal surrogate UQ;
- petroleum conformal forecasting;
- geological robust optimization.

No literature search can prove nonexistence. F6 therefore deliberately uses **“the reviewed literature did not identify”** rather than “no one has ever done.”

---

## 29. Operational rule going forward

Add a lightweight literature-watch task during implementation.

Any newly found paper should be checked against these nine columns:

1. waterflood/petroleum domain;
2. partial observations;
3. recurrent policy;
4. physical CRM/ROM;
5. explicit action projection;
6. measured ROM/full-physics discrepancy;
7. separately calibrated one-sided safety margin;
8. geological calibration/test separation;
9. held-out full-physics realized-constraint evaluation.

A paper matching most of these columns is a priority read and may require F6 to be reopened.
