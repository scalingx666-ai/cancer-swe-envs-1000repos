# Issue

**Title:** Refactor the C code of the GSVA dense random walk

## Description

Refactor the C code of the GSVA dense random walk, after PR #285 by Gabriele Sales (). The code in `src/ks_test.c` has been split in:

* `src/score_genesets.c`: main scoring loop `gsva_score_genesets_R()`
* `src/ranks.c`: fetch columns of the rank and turn them into decreasing order and symmetric rank statistics
* `src/rnd_walk.c`: random walk algorithm

The dense random walk goes now only through the genes in the gene set, reducing the original O(p) computational cost per column to O(k log k), for a gene set of size k.

This PR has been co-authored by Gabriele Sales (gabriele.sales@unipd.it) and Claude Opus 5.5 (noreply@anthropic.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9db994d166da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.