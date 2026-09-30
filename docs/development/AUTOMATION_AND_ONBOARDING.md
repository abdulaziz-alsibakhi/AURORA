# AURORA Automation and Onboarding Architecture

## 1. Purpose

AURORA should teach people how to use AURORA.

A teammate cloning this repository should not need access to another
developer's old workspace, undocumented terminal history, or private
instructions in order to reproduce the project's workflows.

The long-term human entry point will be:

```bash
./aurora
```

This command will provide a guided interface for setup, environment checks,
data preparation, reservoir simulation, experiments, testing, and project
explanations.

The objective is not merely convenience. This is part of AURORA's
reproducibility and software-engineering architecture.

## 2. Core Principle

If a repeatable AURORA procedure requires a person to manually perform a
sequence of technical steps, that procedure should be considered for
documented automation.

The preferred pattern is:

```text
README / documentation
        |
        | explains WHAT and WHY
        v
./aurora
        |
        | guides the user
        v
small documented scripts
        |
        | implement HOW
        v
AURORA software / external tools / generated artifacts
```

Automation must not make the project harder to understand.

A script that nobody understands is not an improvement over a manual
procedure.

## 3. The Human Interface

The planned `./aurora` command is the front door to common project workflows.

A future interface may resemble:

```text
AURORA
Autonomous Reservoir Optimization

What would you like to do?

  1. First-time setup
  2. Check my environment
  3. Reservoir simulation
  4. Prepare datasets
  5. Train / run controller
  6. Run an experiment
  7. View results
  8. Run tests
  9. Explain AURORA
  0. Exit
```

The exact menu may evolve with the project.

The important architectural rule is that the launcher remains a thin
orchestration layer. It should invoke focused scripts or application
components rather than becoming one enormous shell program.

## 4. Two Levels of Use

AURORA should support both beginners and experienced contributors.

### Guided use

A teammate who does not know the workflow can run:

```bash
./aurora
```

The launcher should explain requirements, diagnose the environment, and guide
the person toward the appropriate action.

### Direct use

A contributor who already knows exactly what they need should be able to run
the underlying operation directly, for example:

```bash
./scripts/reservoir/run_egg_opm.sh
```

The guided interface must therefore orchestrate the scripts rather than hide
or duplicate their behavior.

## 5. Script Documentation Contract

Important scripts should be understandable without reverse-engineering them.

Where appropriate, scripts should document:

```text
PURPOSE
    What the script accomplishes and why AURORA needs it.

INPUTS
    Files, arguments, environment variables, or external resources consumed.

OUTPUTS
    Files, directories, data, or state produced or modified.

DEPENDENCIES
    Required programs, packages, services, or datasets.

SAFE TO RERUN?
    Whether the script is idempotent or what repeated execution does.

WORKFLOW
    A short explanation of the major operations.

USAGE
    How a contributor runs the script.
```

Complex workflows should additionally have a README in their script
directory explaining the process conceptually.

## 6. Guided Behavior

Automation should explain failures rather than merely emit cryptic errors.

For example:

```text
[ERROR] Egg Model is not available.

Why this matters:
AURORA needs Egg for controlled reservoir experiments.

How to fix it:
    ./aurora
    -> Reservoir setup
    -> Set up Egg Model

Nothing on your machine was modified.
```

Likewise, environment checks should report useful state:

```text
[AURORA] Environment check

Git                 PASS
Python              PASS
Python environment  PASS
OPM Flow            PASS
Egg Model           NOT CONFIGURED
Volve dataset       PASS
AURORA config       PASS
```

Setup procedures should detect existing valid installations or artifacts
rather than blindly recreating them.

## 7. Planned Automation Structure

The exact structure may evolve as implementation proceeds, but the intended
organization is:

```text
AURORA/
|
|-- aurora
|
|-- scripts/
|   |-- README.md
|   |
|   |-- setup/
|   |   |-- README.md
|   |   |-- check_environment.sh
|   |   `-- setup_environment.sh
|   |
|   |-- reservoir/
|   |   |-- README.md
|   |   |-- setup_egg.sh
|   |   |-- verify_egg.sh
|   |   `-- run_egg_opm.sh
|   |
|   |-- data/
|   |   |-- README.md
|   |   `-- prepare_volve.py
|   |
|   `-- experiments/
|       |-- README.md
|       `-- ...
|
`-- outputs/
    `-- ...
```

These names describe intended responsibilities, not a requirement to create
placeholder implementations before their workflows are known.

## 8. Do Not Automate Unknown Procedures

AURORA must not create scripts simply to make the repository appear complete.

A workflow should first be understood and validated.

Then it can be automated.

```text
understand
    ->
validate manually
    ->
document
    ->
automate
    ->
verify automation
```

Placeholder scripts that imply nonexistent functionality should be avoided.

## 9. External Data and Generated Artifacts

The repository should distinguish between:

1. AURORA source code and configuration;
2. external authoritative datasets or models;
3. reproducible generated artifacts;
4. deliberately preserved evidence.

Large generated workspaces should not be committed merely because they were
created during development.

Whenever practical, the repository should contain the recipe required to
reproduce an artifact rather than a developer's historical copy of that
artifact.

## 10. Egg Model Decision

The historical AURORA feasibility workspace contains a large local Egg
working directory.

That directory will NOT be migrated wholesale into the canonical repository.

Instead, AURORA will preserve:

- authoritative Egg provenance;
- integrity and audit evidence;
- the known simulator input manifest;
- documentation of the required workflow; and
- automation necessary to obtain, verify, prepare, and execute Egg when that
  workflow is finalized.

The intended lifecycle is:

```text
clone AURORA
      |
      v
obtain Egg from authoritative source
      |
      v
verify source / required inputs
      |
      v
prepare simulator inputs
      |
      v
run OPM Flow
      |
      v
generate simulation artifacts locally
      |
      v
AURORA processing / control / evaluation
```

Generated OPM files are outputs, not canonical source material.

## 11. Volve

The same philosophy should be applied to Volve processing.

The immutable source dataset may be preserved where appropriate, while
repeatable transformations should eventually be implemented as documented
scripts.

Derived datasets should be reproducible from the immutable source whenever
practical.

## 12. Reproducibility Goal

Eventually, a clean machine should be able to progress from:

```bash
git clone <AURORA repository>
cd AURORA
./aurora
```

to a functioning AURORA development or experiment environment with as little
undocumented manual intervention as reasonably possible.

Where full automation is impossible or undesirable, `./aurora` should explain
the required manual action and verify its result afterward.

## 13. Contributor Rule

When adding a new repeatable workflow, contributors should ask:

> Would another teammate know how to reproduce this from a fresh clone?

If the answer is no, the workflow is incomplete.

Depending on the task, the solution may require:

- clearer documentation;
- a validation/check command;
- a small script;
- integration into `./aurora`; or
- some combination of these.

The goal is not automation for its own sake.

The goal is understandable, reproducible engineering.
