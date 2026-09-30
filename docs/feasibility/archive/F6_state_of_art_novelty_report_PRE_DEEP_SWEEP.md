# F6 — State-of-the-Art, Gap & Novelty Verification Report

## Verdict: CONDITIONAL PASS — defensible integration gap survives, but broad novelty claims are rejected

## 1. Objective

F6 tests whether AURORA still has a defensible research contribution after comparison with prior work.

The purpose is not to prove that every component is new. It is to identify what is already known, locate the closest prior art, reject invalid novelty claims, and state the narrowest contribution that the current literature search supports.

## 2. Search conclusion

The literature clearly establishes that the following are **not individually novel**:

- reinforcement learning for petroleum-reservoir production optimization;
- reinforcement learning for waterflood control;
- reinforcement learning on the Egg model;
- waterflood optimization under geological uncertainty;
- surrogate-assisted reinforcement learning for waterflooding;
- recurrent/LSTM-style models for reservoir prediction/surrogates;
- safe/constrained reinforcement learning for waterflood production optimization;
- action correction/projection as a safety mechanism in reinforcement learning generally;
- capacitance-resistance models for waterflood prediction and optimization;
- explicit CRM model-error/discrepancy modelling;
- probabilistic CRM forecasting;
- uncertainty calibration/conformal prediction generally;
- hardware-in-the-loop and embedded interlocks generally.

AURORA must not claim novelty for any item above.

## 3. Closest prior-art map

| Prior work / family | What it already establishes | Overlap with AURORA | What it does not establish from the reviewed evidence |
|---|---|---|---|
| Hourfar et al. (2019), *A reinforcement learning approach for waterflooding optimization in petroleum reservoirs* | RL can learn sequential waterflood actions; evaluated on Egg; SIMO/MIMO cases | Egg + RL + waterflood control | Does not establish AURORA's CRM/full-physics mismatch-calibrated safety chain |
| Ma et al. (2019), *Waterflooding Optimization under Geological Uncertainties by Using Deep Reinforcement Learning Algorithms* | DRL waterflood optimization across geological uncertainty | RL + waterflood + geology ensembles | Does not establish AURORA's specific partial-observation recurrent + CRM + calibrated projection architecture |
| Miftakhov et al. (2020), *Reinforcement Learning From Pixels: Waterflooding Optimization* | DRL using pressure/saturation pixel information for injection optimization | RL + reservoir state + injection-rate control | Uses rich simulator-state information rather than AURORA's intended operational partial-observation framing |
| Zhang et al. (2022), *Training effective deep reinforcement learning agents for real-time life-cycle production optimization* | SAC-based sequential real-time well-control policy for life-cycle optimization | DRL + sequential control + real-time policy | Does not establish mismatch-aware CRM/QP/conformal safety integration |
| Mamghaderi et al. (2020/2021), CRM error-model papers | CRM proxy error is real and can be modelled explicitly; time-correlated discrepancy improves forecasts | CRM + model discrepancy/uncertainty | Does not connect CRM discrepancy to recurrent RL action projection with one-sided calibrated safety margins |
| Holanda et al. (2018) and Sayarpour et al. (2009) | CRM/CRMIP are fast waterflood input-output models suitable for optimization | Core reduced-order model family | Not an RL safety architecture |
| MAPIRL (2025), *Multi agent physics informed reinforcement learning for waterflooding optimization* | Physics-informed/multi-agent RL can optimize waterflooding; Egg used as reservoir model | Physics-aware RL + Egg/waterflood | Different controller/safety/UQ contribution |
| Chen et al. (2025), *Worst-Case Soft Actor-Critic-Based Safe Reinforcement Learning Method for Nonlinear Constrained Waterflood Reservoir Production Optimization* | Safe RL for constrained petroleum waterflood optimization already exists; CMDP, safety critic, CVaR/worst-case SAC | Safe RL + petroleum waterflood + explicit constraints | Critically eliminates any claim that AURORA invented safe RL for waterflooding; reviewed description does not show AURORA's CRM/full-physics discrepancy-calibrated projection chain |
| 2026 spatiotemporal surrogate + TD3 waterflood study | High-accuracy spatiotemporal surrogate embedded in DRL; optimized policy re-evaluated in high-fidelity simulator | Surrogate + DRL + simulator re-evaluation | Makes “surrogate + RL + simulator verification” non-novel by itself; no reviewed evidence of AURORA's calibrated safety-margin chain |
| Aghayev et al. (2026), ORACLE | RL-driven adaptive feasibility/constraint learning applied to constrained optimization, with Egg reservoir benchmark material | Egg + RL + learned feasibility/constraint modelling | Strong adjacent prior art; does not from reviewed evidence duplicate the complete AURORA architecture |
| Safe-RL shielding literature under partial observability | Shields can enforce/encourage safe action selection in POMDP settings | partial observation + RL + safety layer | Not petroleum-specific and not AURORA's CRM/full-physics mismatch-calibration mechanism |
| Conformal/probabilistic UQ literature | Data-driven calibrated uncertainty bounds are established methods | calibration concept | Conformal prediction itself is not novel |

## 4. Novelty claims that F6 rejects

AURORA must **not** say:

- “We introduce reinforcement learning to waterflood optimization.”
- “We are the first to apply RL to the Egg model.”
- “We introduce safe reinforcement learning to petroleum waterflooding.”
- “We are the first to optimize waterflooding under geological uncertainty using RL.”
- “We introduce surrogate-assisted RL for reservoir optimization.”
- “We introduce model-error-aware CRM.”
- “We introduce recurrent models to reservoir engineering.”
- “We introduce action projection/shielding to RL.”
- “We introduce conformal prediction.”
- “We introduce QP safety filters.”
- “We introduce hardware-in-the-loop validation.”

These claims are contradicted or made indefensible by existing literature.

## 5. Gap that survives the search

The targeted literature review did **not identify a petroleum-waterflood study that clearly combines all of the following into one evaluated architecture**:

1. operationally restricted / partial observations rather than privileged full simulator state;
2. a recurrent RL controller explicitly used to handle that partial observability;
3. a CRM/CRMIP-style fast waterflood reduced-order model;
4. explicit safety/action projection through a QP-style filter;
5. direct measurement of the CRM/ROM prediction mismatch against a full-physics reservoir simulator;
6. a statistically calibrated **one-sided** margin derived from that measured mismatch and inserted into the safety decision;
7. leakage-safe separation of geological realizations into development/training, calibration, and final held-out testing;
8. final controller comparison on held-out full-physics geological realizations;
9. explicit measurement of the trade-off among constraint violations, safety-filter intervention, and economic/physical performance.

This is the candidate AURORA research gap.

This is a **search-supported absence**, not proof that no such paper exists anywhere. The claim must therefore be worded cautiously.

## 6. Strongest defensible contribution statement

AURORA should frame its contribution approximately as:

> **AURORA investigates an integrated mismatch-aware supervisory-control architecture for sequential waterflood optimization under partial observation. The architecture couples recurrent reinforcement learning with a CRM/CRMIP-style reduced-order reservoir model and an explicit constraint-projection layer, measures reduced-order/full-physics prediction mismatch, converts that measured mismatch into a one-sided statistically calibrated safety margin, and evaluates the resulting controller on held-out full-physics geological realizations.**

The novelty is the **integration and experimental evaluation of this chain**, if implemented successfully.

The novelty is **not** any one component.

## 7. Stronger scientific question

AURORA's most defensible research question is not:

> Can RL optimize a waterflood?

That question has already been answered repeatedly.

A stronger question is:

> **Can a fast reduced-order-model safety projection, augmented by a one-sided margin calibrated from measured reduced-order/full-physics mismatch, reduce realized operational-constraint violations for a recurrent waterflood controller under partial observation and geological uncertainty, while retaining useful economic/production performance on held-out full-physics realizations?**

This question creates falsifiable experimental comparisons.

## 8. Required ablations / comparators

To demonstrate that the proposed integration matters, the final evaluation should separate the contribution into controlled comparisons.

Minimum recommended ladder:

1. fixed Egg schedule;
2. heuristic injection controller;
3. conventional optimization/QP or MPC-style baseline where feasible;
4. PPO;
5. RecurrentPPO;
6. RecurrentPPO + nominal QP projection;
7. RecurrentPPO + mismatch-calibrated QP projection;
8. at least one safe-RL comparator if implementation time permits;
9. oracle/full-information diagnostic where useful, but not as a deployable controller.

Critical ablations:

- PPO vs RecurrentPPO → tests value of recurrence under partial observation;
- R-PPO vs R-PPO + nominal QP → tests projection layer;
- nominal QP vs mismatch-calibrated QP → tests the actual mismatch-calibration contribution;
- calibration vs no calibration across held-out geology → tests whether the margin generalizes;
- controller-visible observations vs privileged/oracle state diagnostic → quantifies cost of partial observability.

## 9. Metrics required to support the contribution

AURORA should report more than reward/NPV.

At minimum:

### Performance
- cumulative oil;
- cumulative produced water;
- cumulative injected water;
- documented economic objective / NPV-style metric;
- episode return.

### Safety / constraint behaviour
- number/rate of realized constraint violations in OPM;
- violation magnitude;
- maximum violation;
- duration of violation where meaningful;
- QP intervention frequency;
- action correction magnitude;
- slack/infeasibility frequency.

### Model mismatch / calibration
- ROM prediction error against OPM;
- signed safety-relevant residual distribution;
- nominal vs empirical one-sided coverage;
- calibrated margin magnitude;
- calibration-set vs held-out-test coverage;
- performance as mismatch increases.

### Generalization
- per-realization results;
- held-out geological aggregate;
- distribution/confidence intervals;
- multiple random seeds for learned policies.

### Computational
- ROM/controller/QP decision time;
- OPM reference-evaluation cost;
- speed difference between reduced-order and full-physics paths.

## 10. Why the CRM mismatch component matters

Prior CRM literature already recognizes that fast CRM proxies carry structural/model discrepancy. Mamghaderi et al. explicitly model time-correlated CRM error and report improved prediction when error is accounted for.

Therefore AURORA cannot claim that discovering CRM error is novel.

The research opportunity is instead to use **empirically measured CRM/full-physics error as an input to the controller's safety margin**, then experimentally test whether this reduces realized full-physics violations without becoming unnecessarily conservative.

That converts a known modelling limitation into an explicit control/UQ experiment.

## 11. Why simulator re-evaluation alone is insufficient novelty

Recent waterflood work already embeds learned surrogates inside DRL and then re-evaluates optimized controls in a higher-fidelity simulator.

Therefore:

`surrogate → RL → simulator re-evaluation`

is no longer a sufficient novelty claim.

AURORA must preserve the additional structure:

`ROM → measured full-physics mismatch → calibration-only residuals → one-sided margin → explicit projection → held-out full-physics test`.

## 12. Why safe RL alone is insufficient novelty

The 2025 SPE Journal WCSAC paper directly applies safe reinforcement learning to nonlinear constrained waterflood production optimization using a constrained MDP, a safety critic, CVaR and adaptive safety weights.

Therefore “safe RL for waterflooding” is definitively occupied prior art.

AURORA's comparison should explain that its proposed safety mechanism is structurally different:

- external/explicit projection rather than only learned constraint satisfaction;
- reduced-order physical proxy in the safety path;
- measured proxy/full-physics discrepancy;
- separate statistical calibration of that discrepancy;
- realized held-out OPM verification.

Whether this different architecture is *better* is an empirical question, not a novelty assumption.

## 13. Partial observability / recurrence

Partial observability is a well-established RL problem, and recurrent policies are a standard response. Reservoir/waterflood literature also contains local-observation and temporal-model approaches.

Therefore recurrence itself is not novel.

Its role in AURORA is experimental: it creates a controller that does not require privileged full-grid simulator state and allows a clean PPO vs RecurrentPPO comparison under the same observation restriction.

The final report should avoid claiming that real fields are exactly represented by AURORA's chosen observation set. It should say the observation design is a controlled approximation of operational information limitations.

## 14. Geological uncertainty

RL waterflood optimization under geological uncertainty predates AURORA. Ma et al. explicitly studied deep RL algorithms for waterflood optimization across geological uncertainty.

Therefore geological ensembles alone are not novel.

AURORA's distinction is the **three-way functional use** of geological realizations:

- development/training;
- mismatch-margin calibration;
- untouched final full-physics testing.

The scientific value depends on preventing leakage among these roles.

## 15. Publication-strength hypothesis

A suitable primary hypothesis is:

> **On held-out Egg geological realizations, a one-sided mismatch-calibrated QP safety projection will reduce the frequency and/or magnitude of realized OPM operational-constraint violations relative to both an unfiltered recurrent RL controller and the same controller with a nominal, uncalibrated QP projection, while retaining more economic/production performance than a uniformly conservative margin chosen without mismatch calibration.**

This is a hypothesis, not an expected result that may be reported as fact.

Possible secondary hypotheses:

- RecurrentPPO performs more robustly than feed-forward PPO under the frozen partial-observation interface.
- CRM/full-physics residuals vary materially across geological realizations, making nominal ROM-only safety predictions insufficient.
- The calibrated margin achieves closer-to-target one-sided held-out coverage than the nominal ROM prediction.
- Safety gains can be characterized as a measurable intervention/performance trade-off rather than a binary safe/unsafe label.

## 16. Demarcation from nearby research

AURORA should distinguish itself from five nearby families:

### Conventional reservoir optimization
Uses full simulators, gradients, evolutionary methods, MPC, or optimization routines. AURORA instead studies learned sequential control plus an explicit safety/UQ architecture.

### Reservoir RL
Already optimizes sequential well controls. AURORA does not claim this as new.

### Safe reservoir RL
Already exists. AURORA investigates a different explicit mismatch-aware projection architecture.

### Surrogate-assisted reservoir RL
Already exists. AURORA specifically treats surrogate/full-physics discrepancy as a calibrated safety quantity rather than only validating surrogate accuracy.

### CRM uncertainty modelling
Already exists. AURORA uses measured discrepancy operationally inside a safety-control evaluation rather than claiming error modelling itself as new.

## 17. HIL novelty boundary

The ESP32-S3/HIL layer should remain an engineering/deployment-validation contribution.

It can make the capstone stronger by demonstrating:

- command/telemetry interfaces;
- timing;
- watchdogs;
- interlocks;
- manual override;
- communication failures;
- fault injection;
- safe failure states.

It should not be used to inflate the research novelty claim unless a genuinely new embedded-control result later emerges.

## 18. Volve novelty boundary

Volve can strengthen external grounding by showing that the relevant kinds of operational time series and CRM-style relationships occur in real field data.

It cannot provide the missing counterfactual outcomes required to prove that AURORA's controller would have outperformed historical operations.

Therefore Volve is supporting realism/grounding, not the main novelty claim.

## 19. Threats to the novelty claim

F6 identifies several threats that must remain visible:

1. **Search incompleteness:** absence from this search is not proof of global absence.
2. **Fast-moving field:** 2025–2026 literature is rapidly adding safe RL, surrogate RL and constraint-learning approaches.
3. **Integration-only weakness:** merely wiring known components together is not enough; the mismatch-calibration mechanism must answer a real scientific question.
4. **No-effect risk:** if calibrated projection behaves identically to nominal QP, the claimed contribution weakens.
5. **Over-conservatism risk:** fewer violations achieved only by collapsing injection/performance is not compelling.
6. **CRM inadequacy risk:** if CRM error is too large/nonstationary for useful calibration, the architecture may require refinement.
7. **Constraint triviality risk:** if the selected pressure/operational constraint is almost never active, the safety experiment is uninformative.
8. **Leakage risk:** calibration or test-geology leakage can invalidate the strongest result.
9. **Comparator risk:** omitting strong safe-RL or optimization baselines can make results difficult to interpret.
10. **Claim-language risk:** words such as “first,” “guaranteed safe,” or “digital twin” can create claims the evidence does not support.

## 20. What would invalidate the F6 gap later?

F6 must be reopened if later literature review finds a petroleum-waterflood paper that already combines substantially the same central mechanism:

- partial-observation recurrent policy;
- CRM/physical ROM;
- explicit constraint projection;
- measured ROM/full-physics residual;
- statistically calibrated one-sided safety margin;
- geological calibration/test separation;
- held-out full-physics safety evaluation.

If such prior work is found, AURORA should compare directly against it and narrow the contribution rather than conceal the overlap.

## 21. Concern decisions

### Concern #12 — Has somebody already done this?

**GREEN with qualification.**

Many pieces have absolutely been done, including Egg RL, geological-uncertainty RL, safe waterflood RL, surrogate-assisted RL, CRM optimization and CRM error modelling.

The reviewed literature did not reveal the complete AURORA mechanism as currently frozen.

### Concern #13 — What exactly is novel/different?

**GREEN with guarded wording.**

The candidate difference is the evaluated integration of:

`partial-observation recurrent control + CRM/CRMIP reduced-order dynamics + explicit safety projection + measured ROM/full-physics mismatch + one-sided statistical calibration + held-out geological full-physics evaluation`.

The contribution must be stated as an integration/methodology/evaluation contribution, not invention of the components.

### Concern #30 — Could this become publishable?

**GREEN as feasibility, not a publication prediction.**

The architecture supports a falsifiable research question and meaningful ablations against established prior art. Publication would still depend on implementation quality, experimental results, statistical evidence, writing, venue fit and peer review.

## 22. F6 Decision

# CONDITIONAL PASS

A defensible research gap survives the state-of-the-art review, but only after aggressively narrowing AURORA's novelty claim.

The project must **not** claim novelty for RL, recurrent RL, safe RL, QP/projection, CRM, CRM error modelling, conformal calibration, geological ensembles, surrogate-assisted optimization, simulator re-evaluation, or HIL individually.

The strongest surviving contribution is the **mismatch-aware integrated supervisory-control architecture and its leakage-safe full-physics evaluation**.

F6 therefore permits progression to F7/G0, subject to continued literature monitoring and conservative novelty language.

## 23. Key literature register

1. Hourfar, F., Jalaly Bidgoly, H., Moshiri, B., Salahshoor, K., & Elkamel, A. (2019). *A reinforcement learning approach for waterflooding optimization in petroleum reservoirs*. Engineering Applications of Artificial Intelligence, 77, 98–116. DOI: 10.1016/j.engappai.2018.09.019.
2. Ma, H., Yu, G., She, Y., & Gu, Y. (2019). *Waterflooding Optimization under Geological Uncertainties by Using Deep Reinforcement Learning Algorithms*. SPE-196190-MS. DOI: 10.2118/196190-MS.
3. Miftakhov, R., Efremov, I., & Al-Qasim, A. (2020). *Reinforcement Learning From Pixels: Waterflooding Optimization*. OMAE2020-18574. DOI: 10.1115/OMAE2020-18574.
4. Zhang, K. et al. (2022). *Training effective deep reinforcement learning agents for real-time life-cycle production optimization*. Journal of Petroleum Science and Engineering, 208, 109766. DOI: 10.1016/j.petrol.2021.109766.
5. Sayarpour, M., Zuluaga, E., Kabir, C.S., & Lake, L.W. (2009). *The use of capacitance–resistance models for rapid estimation of waterflood performance and optimization*. Journal of Petroleum Science and Engineering, 69, 227–238. DOI: 10.1016/j.petrol.2009.09.006.
6. Holanda, R.W., Gildin, E., & Jensen, J.L. (2018). *A generalized framework for Capacitance Resistance Models and a comparison with streamline allocation factors*. Journal of Petroleum Science and Engineering, 162, 260–282. DOI: 10.1016/j.petrol.2017.10.020.
7. Mamghaderi, A., Aminshahidy, B., & Bazargan, H. (2020). *Error behavior modeling in Capacitance-Resistance Model: A promotion to fast, reliable proxy for reservoir performance prediction*. Journal of Natural Gas Science and Engineering, 77, 103228. DOI: 10.1016/j.jngse.2020.103228.
8. Mamghaderi, A., Aminshahidy, B., & Bazargan, H. (2021). *Prediction of waterflood performance using a modified capacitance-resistance model: A proxy with a time-correlated model error*. Journal of Petroleum Science and Engineering, 198, 108152. DOI: 10.1016/j.petrol.2020.108152.
9. Chen, Z. et al. (2025). *Worst-Case Soft Actor-Critic-Based Safe Reinforcement Learning Method for Nonlinear Constrained Waterflood Reservoir Production Optimization*. SPE Journal, 30(12), 7745–7766. DOI: 10.2118/230322-PA.
10. *Multi agent physics informed reinforcement learning for waterflooding optimization* (2025), using the Egg model as a case study.
11. *Spatiotemporal graph-based surrogate modeling and deep reinforcement learning for multi-layer injection-production decision in waterflood reservoirs* (2026). DOI: 10.1016/j.engappai.2026.115452.
12. Aghayev et al. (2026). *ORACLE: Online reinforcement-driven adaptive constraint learning engine for nonlinear optimization*. AIChE Journal. Includes Egg reservoir benchmark material and constrained data-driven optimization.
13. Carr, S., Jansen, N., Junges, S., & Topcu, U. (2022). *Safe Reinforcement Learning via Shielding under Partial Observability*. General safe-RL/POMDP prior art used to prevent overclaiming the partial-observation safety concept.

## 24. Search record

F6 targeted combinations of:

- waterflood + reinforcement learning;
- Egg + reinforcement learning;
- waterflood + safe reinforcement learning;
- waterflood + geological uncertainty + RL;
- waterflood + surrogate + RL;
- CRM + reinforcement learning;
- CRM + model error;
- CRM + uncertainty;
- waterflood + action projection / quadratic programming + RL;
- waterflood + recurrent PPO / LSTM + RL;
- waterflood + partial observability + RL;
- waterflood + conformal prediction;
- petroleum reservoir + conformal uncertainty;
- Egg + constraint learning.

The search was deliberately adversarial: the goal was to find prior art that could destroy AURORA's proposed novelty, not merely papers that support it.
