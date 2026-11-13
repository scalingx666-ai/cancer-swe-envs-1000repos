# Issue

**Title:** perf(bwt): prefetch the first backward-extension occ blocks after a k-mer lookup

## Description

`mb_bwt_smem_batch()` already prefetches occ blocks for every in-flight backward and forward extension step, but the stage 2/5 k-mer-cache lookup is a gap: seeding the interval from `bwt->pre`, and the `mb_bwt_set_intv()` revert, both leave the occ array untouched, so the first backward extension in stage 3/6 starts on cold blocks.

This issues the two prefetches that step will need — `x[0]` and `x[0]+size`, the addresses `mb_bwt_extend()` reads for a backward step — at the end of the lookup stage, so the lines arrive while the entry travels back through the queue. It follows the pattern the four existing prefetch sites already use. Six lines, no new helper, no logic change.

**Output is unchanged** — SAM byte-identical on 100k HG002 WGS pairs.

Mapping-phase wall clock, c8g.4xlarge (Graviton4, 16 vCPU, gcc 11.5), `-t 16`, hs38 with ALT contigs, 5 interleaved reps with build order reversed between reps, per-rep spread 0.29–0.37%:

| dataset | before | after | |
|---|---:|---:|---:|
| 1kg HG00096 WGS, 5M pairs | 41.236s | 40.832s | −1.0% |
| 1kg HG00100 WES, 5M pairs | 18.700s | 18.222s | −2.6% |

The exome gain is the larger of the two, which is what a prefetch fix in the SMEM walk should do: exome spends a bigger share of its time there (~37% of compute self-time vs ~27% for WGS in a sampling profile), so the same per-lookup saving is a bigger fraction of the total.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6d9f87d3009`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.