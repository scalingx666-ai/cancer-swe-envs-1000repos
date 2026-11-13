# Issue

**Title:** Post-1.6.2: Apptainer note and Conda recipe update

## Description

- README: explain that Apptainer is the current name of the open-source Singularity project and runs the same SIF images.
- `conda-recipe/meta.yaml`: move AS-p to 1.6.2 with the release archive hash. It now matches the recipe in the Bioconda PR.

Docs and recipe metadata only. The published 1.6.2 tag and images are unaffected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01C3qw3fKy4EdhryyJxDKHGx

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b6cf5696ddc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.