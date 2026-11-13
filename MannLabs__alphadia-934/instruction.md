# Issue

**Title:** Score protein groups with a logistic regression on the logits of their confident precursors

## Description

# TLDR
https://mannlabs.atlassian.net/wiki/spaces/bioinfo/pages/1524563973/unfuck+protein+fdr+AX-1585

The protein-group MLP (7 features, fit on an 80/20 split) is replaced by a logistic regression on 3 features per group: the mean, best and worst **logit** of the group's precursors at q ≤ 1 %. Groups without such a precursor get `pg_qval = 1`.

Stack: **2/2**, on top of #933 (plain D/T protein q-values). Review that one first.

## Problem
- **Unstable with few decoy groups.** The MLP is fit on an 80 % split. On plasma (~30 decoy groups) its quality varied between seeds from useful to worse than random, and it accepted no group in 2 of 18 benchmark runs.
- **Count features reward false targets in big groups.** `count`, `n_precursor`, `n_peptides` and `n_runs` are taken over every precursor up to `fdr.fdr`. This sums the excess of false targets over decoys into large groups: the groups the MLP added at 5 ng had a marginal FDP of 3–7 %.
- **The probability scale hides the best precursor.** The final-round probabilities of confident precursors span many decades, so on the probability scale every confident target sits at about 0. The group mean then follows the worst precursor, and the model gave the best precursor a negative weight.

## Change
- Features come from precursors with `qval <= 0.01` only (`PROTEIN_FEATURE_QVAL`). Per `(pg, decoy)` they are the mean, min and max of `logit(proba)`. Probabilities are clipped to `[1e-300, 1 - 1e-16]` before the logit.
- A `StandardScaler` plus `LogisticRegression` is fit on all groups, without a split. With 3 features and an intercept there is little to overfit. As a result, train and test in the FDR plot are the same set.
- Groups without a confident precursor get `pg_qval = 1` (`NO_EVIDENCE_QVAL`), so their precursors drop out at the `pg_qval <= fdr.fdr` filter.
- `TooFewProteinsError` is raised when there are no target groups or no decoy groups. In the same situation main fails inside sklearn.
- **Fix:** the FDR plot computed its AUC against labels in pre-sort order, which read about 0.5 (e.g. 0.53 instead of 0.88). It now takes the labels from the sorted frame.

## Behaviour changes to be aware of
- `PROTEIN_FEATURE_QVAL` is fixed at 1 % and does not follow `fdr.fdr`. With `fdr.fdr: 0.1`, a precursor between 1 % and 10 % reaches the output only if its group also has a precursor at ≤ 1 %.
- Groups are ranked only by precursor scores. The number of precursors, peptides or runs no longer counts.

## Evidence
All of this was measured on experiment branches, not on this head:
- **Logit vs probability features:** offline replay of cluster runs, real protein groups at matched FDP in paired entrapment: 200 ng **+10 %**, 5 ng **+4–7 %**, 1 ft unchanged. ⚠️ This was measured on a build whose final-round probabilities were cross-fitted. Main scores the final round in sample, so the effect here may differ.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bd9fbc61d87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.