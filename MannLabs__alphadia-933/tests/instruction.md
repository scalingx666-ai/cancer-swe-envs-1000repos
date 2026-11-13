# Issue

**Title:** Stop rescaling the protein q-values by the target to decoy ratio

## Description

# TLDR
https://mannlabs.atlassian.net/wiki/spaces/bioinfo/pages/1524563973/unfuck+protein+fdr+AX-1585

Protein q-values become the plain decoy-to-target ratio D/T. Main currently multiplies that ratio by `n_targets / n_decoys`, which makes it stricter than its label on large proteomes. On plasma it means no decoy group is ever accepted.

Stack: **1/2**. #934 builds on it.

## Problem
`perform_protein_fdr` multiplies the target-decoy q-values by `n_targets / n_decoys`. Written out, q = D/T becomes (D/n_D) / (T/n_T) = FPR / TPR. The denominator is the whole target population, not the accepted set, so the result does not estimate a false discovery proportion. Accepting even one decoy then requires TPR ≥ 1 / (α · n_decoys):

- **HeLa** (~960 decoy groups): TPR ≥ 10 %. The rule acts like a 0.1 % FDR labelled as 1 %: 8,150 groups, against 9,297 at a plain 1 %.
- **Plasma** (~55 decoy groups): TPR ≥ 182 %. No decoy is ever accepted, so the reported protein count is just the rank of the best-scoring decoy group. Across 18 plasma runs that count had a rank correlation of 0.27 with the number of precursors entering the step and a 29 % CV between replicates of the same file. The plain ratio gives 0.88 and 11 %, and 1,875 groups instead of 591.
- `_build_precursor_table` also filters precursors on `pg_qval`, so on plasma the factor discarded 35 % of the precursors that had already passed precursor FDR.

## Change
- Drop the factor. The q-values are now plain D/T
- `log_protein_fdr_summary` also logs how many decoy groups were accepted. With plain D/T those decoys are the only evidence behind the reported protein FDR.
- New regression test: false targets and decoys are drawn from one score distribution. At the threshold, the accepted set must have a decoy-to-target ratio at or below the threshold and within one decoy of it. The test fails on main (9 decoys over 1,806 targets at a nominal 5 %, so 0.5 % realised) and passes here.

## Caveat
With current decoys, which do not go in as often as false targets, it will appear above nominal FDP by some factor. This will be addressed with stuff like inner decoys and other precursors FDR fixes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bbee520e7cd5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.