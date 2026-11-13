# Issue

**Title:** Add 95% Poisson confidence intervals to TMB output

## Description

## Summary
- Calculate and report 95% Poisson confidence intervals alongside the TMB point estimate
- Add `scipy` dependency to `environment.yml`
- Use explicit keyword args for `scipy.stats.poisson.interval` (avoids deprecated positional `alpha` parameter)
- Guard against division by zero when effective genome size is 0

## Results on test data

| Sample | Variants | TMB | 95% CI Low | 95% CI High |
|--------|----------|-----|------------|-------------|
| test1_mutect2_snpeff | 46 | 1.38 | 0.99 | 1.80 |
| test2_mutect2_snpeff | 769 | 23.11 | 21.48 | 24.76 |
| head_vcf_seqOIA | 434 | 13.04 | 11.84 | 14.27 |

CI width scales inversely with variant count as expected from Poisson statistics. When variant count is 0, both CI bounds report 0.

## Test plan
- [x] Ran all three WES test samples successfully
- [ ] Verify scipy resolves in conda environment

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f061de176416`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.