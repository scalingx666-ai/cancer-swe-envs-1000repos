# Issue

**Title:** Replace zless with zcat for non-interactive VCF filtering

## Description

Replace `zless` with `zcat` for non-interactive VCF filtering in `SpecHLA.sh` (and the same pattern in `test_SpecHLA.sh` and `run.assembly.realign.sh`). `zless` requires a pager (`less`) that is not installed in minimal containers like the bioconda biocontainer, where the script currently fails with `zless: command not found`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c36c600f8e89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.