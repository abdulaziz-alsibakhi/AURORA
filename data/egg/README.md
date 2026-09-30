# Egg Model

The Egg Model is AURORA's synthetic reservoir benchmark for controlled,
counterfactual reservoir-simulation experiments.

AURORA intentionally does not commit the historical Egg working directory or
generated OPM Flow simulation outputs to this repository.

## Authoritative Source

The Egg Model used during AURORA feasibility work was obtained from
TU Delft / 4TU.ResearchData.

Persistent identifier:

https://doi.org/10.4121/uuid:916c86cd-3558-4672-829a-105c62985ab2

Associated publication:

Jansen, J. D., Fonseca, R. M., Kahrobaei, S., Siraj, M. M.,
Van Essen, G. M., & Van den Hof, P. M. J. (2014).
*The Egg Model - A Geological Ensemble for Reservoir Simulation.*
Geoscience Data Journal.

## Why the Dataset Is Not Copied Here

The canonical repository should contain the reproducible procedure needed to
obtain and use Egg rather than a copy of a developer's historical working
directory.

Large OPM-generated simulation files are generated artifacts and should be
recreated when experiments are run.

The historical feasibility evidence required to understand and verify the
original investigation has already been preserved under:

- `docs/feasibility/evidence/F1/`
- `docs/feasibility/evidence/F2/`
- `docs/feasibility/evidence/F3/`

## Known OPM Input Set

The successful F3 feasibility baseline used the following files from the
Eclipse-format Egg model:

- `ACTIVE.INC`
- `COMPDAT.INC`
- `Egg_Model_ECL.DATA`
- `SCHEDULE_NEW.INC`
- `mDARCY.INC`

Their recorded sizes and SHA-256 hashes are preserved in:

`docs/feasibility/evidence/F3/baseline_input_manifest.json`

## Intended Reproducible Workflow

The target workflow is:

```text
obtain Egg
    ->
verify Egg
    ->
prepare required simulator inputs
    ->
run OPM Flow
    ->
generate outputs locally
    ->
AURORA consumes required results
```

This workflow will eventually be exposed through AURORA's guided `./aurora`
interface and implemented using small documented scripts.

Expected responsibilities include:

```text
setup_egg.sh
    Obtain and prepare the required Egg source material.

verify_egg.sh
    Verify that required inputs exist and match expected properties.

run_egg_opm.sh
    Execute the selected Egg case using OPM Flow.
```

These scripts should only be implemented once the corresponding procedures
have been validated. Placeholder scripts should not imply functionality that
does not yet exist.

## Historical Paths

Historical feasibility reports may refer to paths such as:

`data/egg/egg_model_original.zip`

or:

`data/egg/working/Egg_Model_Data_Files_v2/Eclipse`

These describe the temporary September 2026 feasibility workspace.

They are not requirements for the canonical repository layout.

## Egg and Volve Have Different Roles

**Egg + OPM Flow** provide a controlled numerical environment in which AURORA
can evaluate actions and counterfactual controller behavior.

**Volve** provides historical real-field grounding for data analysis and
reduced-order-model plausibility work.

Egg is not represented as real-field data, and historical Volve observations
are not treated as counterfactual ground truth.
