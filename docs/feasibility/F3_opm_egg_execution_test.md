# F3 — OPM–Egg Executability & Counterfactual Control Test

## 1. Purpose

F3 tests whether the Egg reservoir model can serve as a controllable full-physics reference environment for AURORA. It asks whether Egg executes in OPM Flow, useful outputs are machine-readable, a legitimate control can be modified, OPM realizes that modification, and the reservoir trajectory responds measurably.

**F3 decision: PASS.**

## 2. Verified execution environment

- Apple Silicon arm64 host
- linux/arm64 / aarch64 container
- Docker Engine 29.8.0
- OPM Flow 2026.04
- Image: `openporousmedia/opmreleases`
- Immutable digest: `sha256:18c497f6a918c160cd290081d4163abf6e2c349797e18e3b5669c9095044adff`

Evidence: `docs/feasibility/evidence/F3/opm_environment.txt`.

## 3. Egg case

The F2-audited Eclipse-format Egg case contains a 60×60×7 grid, 25,200 total cells, 18,553 active cells, eight water injectors, four producers, and 120 scheduled 30-day periods over 3,600 simulated days. A pristine F3 baseline copy was preserved.

Evidence: `docs/feasibility/evidence/F3/baseline_input_manifest.json`.

## 4. Baseline full-physics execution

The pristine Egg case executed successfully in OPM Flow 2026.04. It completed all 120 report periods, reached 23-Apr-2021, used 128 numerical timesteps, exited with status 0, and produced standard Eclipse/OPM outputs including `EGRID`, `INIT`, `SMSPEC`, `UNSMRY`, and `UNRST`. The unified restart file was approximately 183 MB.

This experimentally achieves AURORA roadmap milestone **0.4 — Full-Physics Hello World**.

## 5. Programmatic output extraction

OPM `summary` successfully extracted:

- Field: `FOPR`, `FWPR`, `FWIR`, `FOPT`, `FWPT`, `FWIT`
- Producers: `WOPR`, `WWPR`, and `WLPR` for PROD1–PROD4
- Injectors: `WWIR` for INJECT1–INJECT8

Evidence: `docs/feasibility/evidence/F3/baseline_summary/`.

Baseline field injection was 636.0. `WWIR:INJECT1` was 79.5 at every report step. Producer oil and water trajectories evolved over time.

## 6. Reservoir-state availability

The generated `UNRST` contains `PRESSURE` and `SWAT`, establishing that pressure and water-saturation state information is present in the full-physics restart output. Convenient pressure summary vectors (`WBHP`, `BPR`, `FPR`) were not requested in the supplied Egg SMSPEC.

Numerical restart-state extraction remains implementation work rather than an F3 blocker.

## 7. Counterfactual control experiment

One active injector command was changed:

- Baseline INJECT1 rate: 79.5
- Perturbed INJECT1 rate: 60.0
- Absolute change: -19.5
- Relative change: -24.528302%

INJECT2–INJECT8 were intentionally unchanged. The 60.0 value is only a feasibility perturbation and is not claimed to be optimal.

Evidence: `control_perturbation.diff` and `counterfactual_input_manifest.json`.

## 8. Perturbed execution and control realization

The perturbed case also completed all 120 report periods and the full 3,600-day horizon with exit status 0.

OPM realized INJECT1 at exactly 60.0 for all report steps, while INJECT2–INJECT8 remained identical to baseline. Total field injection changed exactly as expected:

`636.0 → 616.5`

because `60.0 + 7×79.5 = 616.5`.

Evidence: `docs/feasibility/evidence/F3/perturbed_summary/`.

## 9. Measurable full-physics response

Across 120 report steps:

- Maximum absolute FOPR difference: 19.603852
- Maximum absolute FWPR difference: 39.175797

All four producers responded measurably:

| Producer | Max abs. oil-rate difference | Max abs. water-rate difference |
|---|---:|---:|
| PROD1 | 59.209335 | 19.962847 |
| PROD2 | 13.497124 | 21.662644 |
| PROD3 | 15.145897 | 2.521524 |
| PROD4 | 12.011032 | 2.592778 |

Final cumulative results were:

| Quantity | Baseline | Perturbed | Difference | Relative change |
|---|---:|---:|---:|---:|
| FOPT | 496485.656250 | 494728.875000 | -1756.781250 | -0.353843% |
| FWPT | 1793114.000000 | 1724672.000000 | -68442.000000 | -3.816935% |
| FWIT | 2289600.000000 | 2219400.000000 | -70200.000000 | -3.066038% |

These differences are not interpreted as showing that the perturbed control is better or worse. They prove that a control modification produces quantifiable full-physics consequences.

Evidence: `baseline_vs_perturbed_comparison.json` and `baseline_vs_perturbed_comparison.txt`.

## 10. OPM warning investigation

The pristine Egg deck generated 120 warnings associated with `WELSPECS` inside the `RPTSCHED` reporting request. A diagnostic copy removed only that reporting token while leaving the actual well-definition block untouched.

The warning count fell from 120 to 0. All 13 explicitly tested field/well summary trajectories were byte-identical between pristine and diagnostic runs. `EGRID`, `INIT`, `UNSMRY`, and `UNRST` were SHA-256 identical. `SMSPEC` differed at binary metadata level, but its available vector list was identical.

The evidence supports treating this as an OPM reporting-compatibility cleanup with **no observed effect on the tested numerical reservoir results**. The pristine source remains unchanged.

Evidence: `welspecs_warning_root_cause.txt` and `warning_cleanup_equivalence/`.

## 11. Reproducibility lesson

An exploratory invalid `summary -v` invocation demonstrated that redirected empty files can exist even when a command fails. Invalid evidence was discarded and regenerated.

The permanent experiment runner must therefore validate, in order:

`successful exit → expected file exists → non-empty → expected variables → expected report-step count → analysis → PASS/FAIL`.

The final counterfactual comparison enforced 120 report steps and explicit control realization before declaring PASS.

## 12. What F3 proves

F3 establishes that Egg executes successfully in OPM Flow; the full scheduled horizon can run; field and well trajectories are machine-readable; pressure and saturation state information exists in restart output; an active injector control can be programmatically changed; OPM realizes that change; unchanged injector controls remain unchanged; oil and water trajectories respond; and field/producer/cumulative consequences can be quantified.

The central F3 uncertainty is therefore closed:

> **AURORA can interact with Egg as a controllable full-physics experimental environment rather than merely replaying a fixed reservoir simulation.**

## 13. What F3 does not prove

F3 does not establish that the 60.0 setting is desirable or optimal, that any RL controller improves performance, that RecurrentPPO outperforms PPO, that the reduced-order model accurately reproduces OPM, that the QP layer improves safety, that mismatch calibration is valid, that results generalize across held-out geology, or that Volve historical data demonstrates counterfactual improvement.

OPM is AURORA's **full-physics/high-fidelity reference simulator**, not literal real-world ground truth.

## 14. Remaining non-blocking implementation work

Useful later work includes numerical extraction of `PRESSURE` and `SWAT`; authoritative verification of exact keyword semantics/engineering units before labeling all raw deck values; encoding the validated Egg/OPM compatibility cleanup reproducibly; strict validation in the permanent experiment runner; and extension across the geological ensemble.

None prevents the F3 feasibility decision.

## 15. F3 Decision

# PASS

The demonstrated chain is:

`Egg case → OPM full-physics execution → machine-readable outputs → programmatic injector-control modification → successful counterfactual execution → verified control realization → measurably different field/producer trajectories → quantifiable cumulative differences`.

No F3 result requires abandonment or redesign of AURORA's planned use of Egg and OPM Flow.

**Next: F4 — AURORA Input–Output & Data Sufficiency Traceability Matrix.**
