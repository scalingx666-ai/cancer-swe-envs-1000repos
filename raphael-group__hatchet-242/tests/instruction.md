# Issue

**Title:** Model selection patch

## Description

1. Likelihood-based model-selection approach, replace legacy objective value based approach to handle observation noises. ghostprop and 
2. refactor codes in compute_cn, clean up redundant codes.
3. in run_diploid and run_tetraploid, additionally return scaling factors gamma.
4. allow user to use option `compute_cn.model_select` to decide whether use old or new model-selection method by setting `model_select=likelihood` or `model_select=objective`, respectively.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `39b9ffab10e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.