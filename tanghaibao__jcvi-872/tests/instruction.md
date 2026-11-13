# Issue

**Title:** perf(blastfilter): stream BLAST in two C-score passes to cut memory

## Description

, together with #871 (liftover).

## Problem
`blastfilter_main` did `sorted(list(Blast(...)))`, holding every BLAST line as a `BlastLine` object, about 745 bytes per line. For the reporter's 67M-line LAST file that's about 50 GB, even though only 139K lines survive the C-score filter.

## Fix
When `--cscore` is set (it's 0.7 by default and in `catalog ortholog`), the BLAST file is streamed twice:
1. Record each gene's best score.
2. Keep only lines with `score / max(best[q], best[s]) > cscore`.

Sorting, dedup to the best hit per pair, and the tandem filter then run on the survivors.

Why the output is unchanged:
- Previously, dedup kept each pair's best HSP and then the C-score was computed. A pair's best HSP sets the same per-gene best scores whether or not the other HSPs are present.
- Lower HSPs of a pair can't pass the cutoff when its best one fails, and they're deduped anyway.
- Ties keep file order, because the stable sort runs over the survivors in file order.

Refactoring:
- Line parsing and normalization move to `iter_blasts`; missing-gene warnings are only logged on the first pass.
- `--exclude` is applied while streaming.
- With `--cscore=0`, the single-pass behaviour is unchanged.

## Testing
Output compared byte-for-byte against main:

| Case | Lines out | Output | Peak RSS main → PR |
| --- | --- | --- | --- |
| 1M-line synthetic LAST, default `--cscore=0.7` | 253,545 | identical | 1019 → 619 MB |
| same, `--cscore=0` | 130,043 | identical | 1182 → 1188 MB |
| same, `--exclude` | 244,884 | identical | 1029 → 602 MB |
| self-self version | 217,416 | identical | 1007 → 608 MB |
| real `lastal` output | 292 | identical | — |

The synthetic data keeps about 25% of lines after the C-score filter. In #803 only 0.2% survived, so the real saving there is far larger. The new `test_blastfilter_main` pins best-HSP dedup, the C-score cutoff and `--exclude`; it passes on both main and this branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_019mN8ixeibi7qiB4PzhMo1Y

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63518f7e9c87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.