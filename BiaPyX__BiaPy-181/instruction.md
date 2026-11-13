# Issue

**Title:** Add 'biapy create-config': create a configuration adapted to the data

## Description

This PR adds `biapy create-config` / `biapy.create_config()` to create a configuration from the data, as the wizard does. The data is checked as `check-data` does, and the configuration is built and written with the wizard's `build_config` and `write_config`.

```bash
biapy create-config --workflow SEMANTIC_SEG --ndim 2D --train-raw <x> --train-gt <y> [--test-raw <x>] [--test-gt <y>] [--quick] [--store config.yaml] [--json]
```

It returns the configuration and the wizard's summary of what it decided. If the data can't be used, it returns the errors and no configuration.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7eac9dd7b255`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.