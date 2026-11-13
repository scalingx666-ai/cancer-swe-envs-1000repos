# Issue

**Title:** fix(upload): block scRNA-seq uploads with fewer than 100 cells

## Description

Devel port of fix 1 from #1920 (master hotfix).

A pseudo-bulk matrix with a handful of columns, uploaded as scRNA-seq, passes the counts checks and then fails downstream: QC/BC t-SNE ("perplexity is too large"), Azimuth (`k.score` > n cells), and `pgx.createSingleCellPGX` (`dim(X) must have a positive length`). Seurat's t-SNE (perplexity 30) needs more than 91 cells. Uploads with fewer than 100 cells now stop at step 1 with a message pointing to RNA-seq, next to the existing 200k max-cells stop.

The other half of #1920 (one-sample groups getting DESeq2 back after the compute UI re-renders) is already on devel via #1918, so it isn't included here.

Clean cherry-pick onto devel; the surrounding block is identical to master's. Tested in the app on master only.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1367c67eebe5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.