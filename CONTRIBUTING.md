# Contributing

AURORA should remain reviewable, reproducible, and understandable by the whole team.

## Workflow

For meaningful work: begin from a GitHub Issue, create a descriptive branch, make focused changes, verify them, open a pull request, obtain review when appropriate, and merge with the issue linked. Important work should not exist only on one person's machine or only in Discord.

Suggested branch names include `simulation/egg-opm-setup`, `controller/rppo-baseline`, `safety/qp-baseline`, `domain/volve-characterization`, `experiments/model-mismatch`, and `docs/proposal-requirements`.

Commit messages should describe the engineering change, for example `docs: define validation criteria`, `simulation: add reference configuration`, or `safety: add baseline constraints`.

## Pull requests

Explain what changed, why, how it was verified, which issue it addresses, and remaining limitations. Evidence can include tests, experiment output, plots, screenshots, or documentation.

## Large files and secrets

Never commit credentials, API tokens, private keys, raw multi-GB datasets, large simulator output directories, or large checkpoints simply for convenience. Follow `data/README.md` and `artifacts/README.md`.
