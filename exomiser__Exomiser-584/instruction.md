# Issue

**Title:** Enhancement/html report

## Description

- Updating bootstrap inline css and scripts (so it can be used offline)
- Reworking main gene scores to collapsed accordions
- making filtering steps clearer
- use graph for variant distributions
- No updates to the settings tab
- Genescores disease list shows scores with colors based on 3rds
- Genescores variant analysis shows information in cards with relative score colors
- migrating top transcript interpretation to the accordion level

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8b8eff95050`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.