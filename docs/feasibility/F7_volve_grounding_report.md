# F7 — Volve Real-Field Grounding Feasibility Report
## FINAL DEEP-AUDIT VERSION

## Verdict

# PASS FOR THE DEFINED GROUNDING ROLE

Volve is suitable for AURORA's defined real-field-grounding role.

It is **not** suitable, from historical observations alone, for proving that an AURORA controller would have produced superior counterfactual field outcomes.

That boundary is essential to the PASS.

---

## 1. Purpose

F7 tests whether AURORA can connect its controlled Egg/OPM research environment to genuine field data without making an invalid leap from simulation to real-world controller proof.

The frozen architecture assigns different evidentiary roles:

- **Egg + OPM:** controlled counterfactual full-physics experiments;
- **Volve:** real-field data grounding, CRM/CRMIP plausibility, operational-variable realism, preprocessing/data-quality experience, and comparison with a released history-matched field model where useful;
- **ESP32/HIL:** deployment/control-system behaviour.

F7 therefore does not ask whether Volve can replace Egg. It asks whether Volve can credibly demonstrate that important pieces of AURORA correspond to real reservoir operations.

---

## 2. Official provenance and access

Equinor publicly released the Volve field dataset for research, study and development.

Equinor states that:

- the release covers subsurface and operating data from the Volve field;
- the dataset contains approximately 40,000 files;
- Volve produced from 2008 to 2016;
- students, academic institutions and researchers may use the dataset under the Equinor Open Data Licence without requesting an additional permission letter.

The Norwegian Offshore Directorate independently identifies Volve as a North Sea field, discovered in 1993, producing from 12 February 2008 until 21 September 2016, and now shut down.

**Decision: VALIDATED.**

AURORA has a legitimate public real-field source with authoritative provenance.

---

## 3. Licence

The Equinor Volve licence grants a worldwide, royalty-free, non-exclusive licence to download and use the licensed material, including creation/reproduction of adapted material, subject to the licence terms.

AURORA must preserve the Equinor licence file and attribution/provenance information.

The project should not assume that “open data” means unrestricted relicensing of the raw source files. Any redistribution or publication of derived material must follow the actual licence terms.

**Decision: VALIDATED WITH LICENCE-COMPLIANCE REQUIREMENT.**

The licence does not block academic capstone/research use.

---

## 4. What Volve contains

The official release is far broader than the small production spreadsheet.

Relevant categories include:

- daily and monthly production data;
- well logs;
- well technical data;
- drilling information;
- seismic data;
- geological/subsurface data;
- production/operating data;
- reservoir simulation models;
- Eclipse dynamic-model input and result data;
- RMS geological models;
- reports, including field-development/reservoir-model material.

The released reservoir-model package has been independently used in peer-reviewed research and described as containing a functional, history-matched simulation model.

**Decision: VALIDATED.**

Volve provides substantially more grounding evidence than a production-rate CSV alone.

---

## 5. Production-data structure

Independent inspections of the standard `Volve production data.xlsx` report:

### Daily Production Data

Approximately **15,634 rows × 24 columns**.

Relevant fields include:

- `DATEPRD`
- `WELL_BORE_CODE`
- `NPD_WELL_BORE_CODE`
- `NPD_WELL_BORE_NAME`
- `ON_STREAM_HRS`
- `AVG_DOWNHOLE_PRESSURE`
- `AVG_DOWNHOLE_TEMPERATURE`
- `AVG_DP_TUBING`
- `AVG_ANNULUS_PRESS`
- `AVG_CHOKE_SIZE_P`
- `AVG_WHP_P`
- `AVG_WHT_P`
- `DP_CHOKE_SIZE`
- `BORE_OIL_VOL`
- `BORE_GAS_VOL`
- `BORE_WAT_VOL`
- `BORE_WI_VOL`
- `FLOW_KIND`
- `WELL_TYPE`

### Monthly Production Data

Approximately 527 usable records in recent independent inspections, with fields including:

- well identity;
- year/month;
- on-stream duration;
- oil;
- gas;
- water;
- water injection;
- gas injection.

Small row-count differences reported by third-party readers (for example 527 versus 529 depending on parsing/blank rows) must be resolved by auditing AURORA's own official copy rather than hard-coding a third-party count.

**Decision: VALIDATED.**

The data contains the central historical signals required for real-field CRM-style analysis: time, injection, production, well identity, operating status, and several pressure/operational variables.

---

## 6. Missing-data reality

Volve is real operating data and is not perfectly complete.

Independent inspection of the daily spreadsheet reports:

- `ON_STREAM_HRS`: 285 missing of 15,634;
- `AVG_DOWNHOLE_PRESSURE`: 6,654 missing (~42.6%);
- `AVG_DOWNHOLE_TEMPERATURE`: 6,654 missing;
- `AVG_ANNULUS_PRESS`: 7,744 missing;
- `AVG_CHOKE_SIZE_P`: 6,715 missing;
- `AVG_WHP_P`: 6,479 missing;
- `BORE_WI_VOL`: absent on many rows because many rows are not injector observations;
- oil/gas/water volumes similarly have role-dependent missingness.

At least one independent exploration reports 100% missing downhole pressure for F-5 in the commonly used production table.

These missing values are not automatically data corruption. Some arise because variables are inapplicable to a well/role/time, while others reflect measurement availability.

AURORA must classify missingness by:

1. well;
2. date;
3. well role;
4. variable;
5. operational status.

It must not globally mean-fill, zero-fill, or drop all incomplete rows without engineering justification.

**Decision: VALIDATED WITH DATA-QUALITY CONDITION.**

Missingness is material but does not invalidate the grounding role.

---

## 7. Waterflood relevance

Volve is directly relevant to waterflooding.

Published field studies describe water injection sustaining production and identify F-4 and F-5 as major water-injection wells over substantial portions of the operating history. Approximately 3×10^7 Sm³ of formation water injection has been reported in peer-reviewed work.

The production spreadsheet contains `BORE_WI_VOL`, while producer histories contain oil/water/gas volumes.

**Decision: VALIDATED.**

Volve is not merely an oil-production forecasting dataset; it contains real injection-response information relevant to waterflood analysis.

---

## 8. Well identities and changing roles

Well roles cannot safely be treated as one permanent label.

The Norwegian Offshore Directorate provides authoritative wellbore-purpose records for Volve development wells.

Published Volve reservoir studies also note that F-5, initially used as an injector, was later converted to production.

Therefore AURORA must build a **time-aware well-role table**.

Required representation:

`well + start_date + end_date + role + source`

rather than:

`well -> permanent role`.

This matters directly to CRM fitting because injection and production signals must be assigned according to the role active at each time.

**Decision: VALIDATED; STATIC ROLE ASSUMPTION REJECTED.**

---

## 9. Direct precedent for CRMIP on Volve

This is the strongest evidence for F7.

Nikitin, Revin, Hvatov, Vychuzhanin and Kalyuzhnaya (2022), in *Computers & Geosciences*, used the Volve dataset as a real-field case study and explicitly selected **CRMIP (Capacitance–Resistance Model Injector–Producer)** as the physics-related model for oil-production forecasting.

The paper compares:

- physics-related CRMIP;
- pure data-driven forecasting;
- hybrid CRM + machine-learning approaches.

The authors state that the Volve **production-data portion** was used for the CRM model.

**Decision: STRONGLY VALIDATED.**

AURORA's proposal to use Volve to demonstrate real-field plausibility of its CRM/CRMIP layer has direct peer-reviewed precedent.

This does not mean AURORA should reproduce that paper's exact preprocessing or claim its results.

---

## 10. Reservoir simulation model and history matching

The Volve release contains Eclipse reservoir-model input and result data.

Peer-reviewed literature describes the released dataset as containing a functional reservoir simulation model that had already been history matched.

Other research has:

- imported Volve model properties into other simulators;
- compared simulated production with historical field production;
- performed additional/alternative history matching;
- used Volve as a benchmark for assisted history matching and reservoir-model studies.

A published dataset derivative also provides the released 2016 Eclipse PRT output (~238.7 MB), although AURORA should prefer the official Equinor source when obtaining primary data.

**Decision: VALIDATED.**

This provides an optional bridge between real historical data and reservoir-simulation behaviour.

However, the released model must not be treated as exact subsurface truth.

---

## 11. What Volve can validate for AURORA

Volve can credibly support the following claims if AURORA actually performs the corresponding analysis:

### A. Operational-variable realism
Real field records contain:
- water injection;
- oil/water/gas production;
- well identities;
- on-stream time;
- pressure-related measurements;
- choke/operating variables.

### B. CRM/CRMIP fitting feasibility
There is direct published precedent for fitting CRMIP-family models using Volve production data.

### C. Real injector-producer temporal relationships
AURORA can estimate CRM connectivity/time constants from historical injection-production behaviour, subject to identifiability/data-quality limitations.

### D. Data-engineering realism
Volve exposes:
- missing data;
- role changes;
- shut-ins;
- uneven operating periods;
- nonstationarity;
- changing controls;
- real measurement limitations.

### E. Simulator/field context
The released history-matched Eclipse model can be used for contextual comparison where technically appropriate.

### F. Plausibility of AURORA's observation design
The real production file demonstrates that many of the proposed well-level signals correspond to measurements or operating records that exist in an actual field dataset.

---

## 12. What Volve CANNOT validate

Historical Volve observations cannot reveal what the field would have done under arbitrary AURORA actions that were never executed.

Therefore Volve historical data alone cannot prove:

- AURORA would have produced more oil;
- AURORA would have increased NPV;
- AURORA would have reduced violations;
- the QP would have prevented a historical unsafe condition;
- RecurrentPPO would have selected better actions;
- the calibrated margin would have improved historical field operations;
- the controller is safe for field deployment.

Those are counterfactual claims.

**Decision: HARD CLAIM BOUNDARY.**

Controlled controller comparisons belong in Egg/OPM.

---

## 13. Why the released Volve simulator does not erase the boundary

A history-matched Volve reservoir model can generate counterfactual simulations, but those outputs are still **model-based counterfactuals**, not observed alternate histories.

Therefore AURORA may say:

> “We evaluated an alternative control in a Volve-derived/history-matched simulation model.”

It may not say:

> “This proves the real Volve field would have responded this way.”

For the frozen AURORA scope, Volve need not become a second controller benchmark. Egg/OPM remains the clean controlled experimental platform.

Attempting to make Volve a second full controller-validation environment could materially expand scope and simulator-conversion work without being necessary for feasibility.

---

## 14. Recommended F7 implementation experiment

The minimum useful Volve grounding experiment should be deliberately modest and reproducible.

### Stage 1 — provenance and inventory

Record:
- official source;
- download/access date;
- licence hash;
- production-file hash;
- file sizes;
- sheet names;
- columns;
- units where documented.

### Stage 2 — production audit

For each well:
- date range;
- role by time;
- active days;
- injection volume availability;
- oil/water/gas volume availability;
- pressure-variable availability;
- missingness;
- zero/nonzero intervals;
- role transitions.

### Stage 3 — time normalization

Choose a defensible common interval, likely daily or monthly depending on data quality.

Do not interpolate long shut-ins or missing operating periods as if the well operated continuously.

### Stage 4 — CRM/CRMIP feasibility subset

Select periods with:
- known active injectors;
- active producers;
- adequate overlap;
- sufficient variation/excitation in injection;
- acceptable production data completeness.

### Stage 5 — fit CRM/CRMIP

Estimate:
- injector-producer connectivity/gain terms;
- time constants;
- any selected BHP/production terms required by the chosen formulation.

### Stage 6 — temporal validation

Use a chronological holdout.

Do not randomly shuffle time-series observations.

Report:
- MAE/RMSE or suitable rate metrics;
- cumulative-production error;
- residual behaviour;
- stability/plausibility of parameters;
- sensitivity to preprocessing.

### Stage 7 — comparison to trivial baselines

At minimum compare CRM against:
- persistence/last-value;
- simple moving-average or similarly transparent temporal baseline.

Optional:
- a small data-driven model if useful.

The purpose is not to win a forecasting competition. It is to demonstrate that the physical ROM family can be fitted to genuine field histories and to characterize its limitations.

---

## 15. CRM identifiability / causality guardrails

A fitted CRM connectivity coefficient is a model parameter, not automatic proof of a unique geological flow path.

Injection and production may be affected by:

- common field-management decisions;
- changing BHP/choke conditions;
- shut-ins;
- producer/injector conversions;
- facility constraints;
- faults and heterogeneous connectivity;
- simultaneous changes in several wells;
- limited excitation;
- measurement noise.

Therefore AURORA should describe CRM terms as **estimated dynamic interwell influence/connectivity within the fitted model**, not direct geological proof.

Simple correlation between an injector and producer is insufficient to establish causality.

---

## 16. Pressure-data guardrail

Volve pressure-related variables are valuable for grounding AURORA's observation design, but their missingness is substantial.

AURORA must not design its Volve CRM experiment around complete downhole-pressure histories unless the actual official data audit confirms adequate coverage for the selected wells/period.

Possible defensible choices:

- fit a rate-based CRM subset;
- include BHP only where coverage supports it;
- analyze pressure availability separately;
- use wellhead/choke variables only if physically justified for the chosen analysis.

Do not silently impute pressure across long missing intervals.

---

## 17. Time-resolution guardrail

Daily data is richer but noisier and more operational.

Monthly data is easier to align and has precedent in Volve analyses but loses fast dynamics.

AURORA should choose resolution based on:

- overlap among injectors/producers;
- CRM response times;
- missingness;
- control-change frequency;
- numerical stability.

The final report must state the chosen aggregation rule.

Monthly aggregation must preserve volumes/rates correctly; totals must not be accidentally averaged where sums are required.

---

## 18. Unit guardrail

Volve contains quantities expressed in field-data units such as Sm³ and pressure units such as bar.

AURORA must create a machine-readable unit map and normalize quantities before combining data sources.

Required checks:

- volume versus rate;
- daily volume versus average daily rate;
- stock-tank/standard conditions;
- pressure units;
- time-base conversions;
- cumulative versus interval quantities.

No CRM fit should proceed until the unit contract is explicit.

---

## 19. Well-name normalization

The dataset contains multiple representations of wells/wellbores.

AURORA should preserve:

- raw name;
- NPD/SODIR identifier where available;
- normalized internal identifier;
- bore/side-track distinction.

Do not merge `F-1`, `F-1 B`, and `F-1 C` merely because their names share a stem.

Normalization must be evidence-based.

---

## 20. Data leakage

For Volve forecasting/CRM validation:

- fit on earlier history;
- validate on later history;
- keep preprocessing parameters fit only on the training period where applicable.

Do not randomly split individual daily rows across train/test.

This is separate from Egg's geological-realization leakage problem, but the same scientific principle applies.

---

## 21. Relationship to Egg

Egg and Volve should remain complementary rather than forced into one model.

### Egg/OPM answers
“What happens under an alternative action in a controlled full-physics benchmark?”

### Volve answers
“Do the model inputs, operational signals and CRM-style relationships have grounding in real field histories?”

The reservoirs differ in:
- geometry;
- wells;
- geology;
- fluids;
- operating history;
- measurements;
- uncertainty.

A CRM fitted on Volve is not transferred numerically to Egg as if the reservoirs were interchangeable.

The shared object is the **modeling methodology**, not the fitted parameters.

---

## 22. Relationship to F6 novelty

Volve does not create the central AURORA novelty.

Indeed, CRMIP on Volve is already published prior art.

Its role is stronger scientific grounding:

- the CRM family is not only a synthetic-Egg convenience;
- the relevant production/injection histories exist in a real field;
- real data exposes limitations absent from a clean simulator benchmark.

This strengthens external relevance without inflating novelty.

---

## 23. Data downloads actually required

### Required for implementation of F7

AURORA ultimately needs an official Equinor copy of the Volve production data, specifically the package containing:

`Volve production data.xlsx`

If the current `data/volve` directory already contains the official production workbook/package, **do not redownload it**.

### Already present in AURORA

F1 recorded:

`references/volve/Equinor_Volve_Data_Licence.pdf`

Keep it.

### Optional, not required for F7 PASS

The full Volve release is several orders of magnitude larger than the production spreadsheet and is unnecessary merely to prove CRM grounding.

Do **not** download the entire ~40,000-file release just for F7 unless AURORA later commits to a deeper Volve simulation/model experiment.

Optional later items:
- Eclipse reservoir model;
- model/history-match documentation;
- well reports;
- seismic;
- well logs.

These are useful research resources, not current hard dependencies.

---

## 24. Evidence package to create when the workbook is local

Recommended F7 evidence:

`docs/feasibility/evidence/F7/volve_source_manifest.json`

`docs/feasibility/evidence/F7/volve_production_schema.json`

`docs/feasibility/evidence/F7/volve_well_role_timeline.csv`

`docs/feasibility/evidence/F7/volve_missingness.csv`

`docs/feasibility/evidence/F7/volve_date_coverage.csv`

`docs/feasibility/evidence/F7/volve_units.json`

`docs/feasibility/evidence/F7/volve_audit.log`

Later implementation:

`artifacts/volve/crm_fit/`

The feasibility report itself does not require pretending those implementation artifacts already exist.

---

## 25. Concern #1 — Can we access enough oil/reservoir data?

# GREEN

Official Volve data is publicly available for research/study/development under Equinor's licence, and the release is extensive.

---

## 26. Concern #3 — Is the data good enough?

# GREEN WITH NORMAL REAL-DATA LIMITATIONS

The relevant injection/production/operational signals exist and have already supported peer-reviewed CRMIP and reservoir-model research.

The dataset has substantial missingness in some pressure/operational variables and requires disciplined preprocessing.

“Good enough” does not mean complete or noise-free.

---

## 27. Concern #9 — Does AURORA solve a real problem?

# GREEN AS GROUNDING EVIDENCE

Volve demonstrates that real field operations contain time-varying injection, production, pressure and operational histories of the kind AURORA models.

It does not by itself prove the proposed controller improves real operations.

---

## 28. Concern #11 — Reservoir-engineering grounding

# IMPROVED, BUT F5 CLOSURE CRITERIA STILL APPLY

The Volve evidence strengthens Concern #11 substantially:

- genuine waterflood/injection histories exist;
- CRMIP has direct peer-reviewed Volve precedent;
- a released history-matched reservoir model exists;
- real data exposes operational complications such as missing pressure and changing well roles.

However, F5's implementation-level closure criteria remain:
- exact Egg pressure extraction;
- final safety-limit interpretation;
- CRM oil/water formulation;
- final action bounds.

F7 does not magically close those Egg implementation tasks.

---

## 29. Concern #28 — Can we demonstrate reservoir engineering without a real reservoir?

# GREEN

AURORA has a defensible evidence ladder:

1. controlled synthetic geological ensemble (Egg);
2. full-physics reference simulation (OPM);
3. genuine historical field grounding (Volve);
4. deployment/control-system analogue (HIL).

The project does not need access to a live producing reservoir to demonstrate reservoir-engineering substance.

---

## 30. Risks

| Risk | Consequence | Mitigation |
|---|---|---|
| Full Volve dataset is huge | Scope/storage/time explosion | Download only required official subsets |
| Production data has missing values | Biased/invalid CRM fit | Missingness audit by well/time/role |
| F-5 changes role | Wrong injector/producer mapping | Time-aware role timeline |
| Pressure incomplete | Invalid pressure-based real-data claims | Rate-based CRM where necessary; report coverage |
| Operational confounding | CRM coefficient overinterpreted as geology | Use cautious dynamic-influence language |
| Historical data lacks counterfactuals | Invalid controller-performance claim | Keep controller proof in Egg/OPM |
| History-matched model mistaken for truth | Overclaiming | Call it a calibrated/model-based representation |
| Unit/aggregation mistakes | Physically meaningless fit | Freeze unit contract and aggregation rules |
| Random temporal split | Leakage | Chronological holdout |
| Entire Volve scope expands project | Schedule risk | Keep F7 grounding narrow |

---

## 31. Final F7 decision

# PASS FOR THE DEFINED GROUNDING ROLE

No fatal Volve-data dependency was found.

The official release provides:
- authoritative provenance;
- permissive research access;
- real water-injection and production histories;
- operational/pressure variables;
- well identities;
- reservoir-model resources;
- enough history to support real-field CRM/CRMIP grounding.

Most importantly, peer-reviewed work has already demonstrated CRMIP-family modelling using the Volve production data.

The limitations are well defined:
- missing pressure/operational measurements;
- time-varying well roles;
- operational confounding;
- historical counterfactual impossibility;
- history-matched simulation is model evidence, not alternate observed reality.

These limitations do not invalidate AURORA's frozen Volve role.

**F7 is therefore complete at feasibility level.**

---

## 32. Key external evidence

1. Equinor, **Volve field data set** — official dataset/access/licence page.
2. Equinor, **Terms and Conditions for Use of License to Data — Volve**.
3. Norwegian Offshore Directorate, **Volve field fact page**.
4. Nikitin, N.O., Revin, I., Hvatov, A., Vychuzhanin, P., & Kalyuzhnaya, A.V. (2022). **Hybrid and automated machine learning approaches for oil fields development: The case study of Volve field, North Sea.** *Computers & Geosciences*, 161, 105061. DOI: 10.1016/j.cageo.2022.105061.
5. **Ensemble Machine Learning Assisted Reservoir Characterization Using Field Production Data — An Offshore Field Case Study** (2021), *Energies*, 14, 1052 — Volve history-matched model and field-production use.
6. **Comparison of map metrics as fitness input for assisted seismic history matching** (2022), *Journal of Geophysics and Engineering* — describes the released Volve functional reservoir simulation model as already history matched.
7. Equinor Volve dataset documentation — production data includes daily/monthly well data and reservoir-model Eclipse/RMS material.
8. Peer-reviewed Volve studies confirming water-injection history and use of F-4/F-5.
9. Independent reproducible inspections of `Volve production data.xlsx` used only to corroborate schema/missingness; AURORA must audit its own official copy before freezing exact counts.

---

## 33. G0 carry-forward

F7 removes Volve access/grounding as a feasibility blocker.

G0 must retain these claim boundaries:

- **Egg/OPM:** controlled counterfactual evidence.
- **Volve:** historical real-field grounding.
- **OPM:** full-physics/high-fidelity reference, not literal real-world ground truth.
- **Volve historical observations:** no unobserved counterfactual controller proof.
- **History-matched Volve simulator:** model-based counterfactual evidence only.
- **HIL:** deployment/control-system validation, not reservoir physics.

Next: **G0 — Final Feasibility & GO/NO-GO Dossier.**
