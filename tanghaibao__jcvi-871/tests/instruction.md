# Issue

**Title:** perf(synteny): stream BLAST in liftover to cut memory

## Description

Part of #803: fixes the liftover step. The blastfilter step's memory use is still open.

## Problem
`process_blast_for_liftover` built four structures with one entry per BLAST line: `seen` (a set of name tuples), `accepted` (a dict of name tuples to score strings), `blast_to_score` (a dict of index pairs to scores) and `all_hits` (lists of tuples). That's about 700 bytes per line, so the reporter's 67M-line LAST file needed about 45 GB. #809 only partly fixed it; the reporter still saw 37.8 GB.

## Fix
Read the anchors before streaming the BLAST file, and keep only what liftover uses:
- `accepted` only for anchor pairs; lifted pairs are added as they are lifted.
- Hits only for chromosome pairs that have anchors, stored as compact `array("q")` (qi, si, score) rows, about 24 bytes per HSP.
- The first HSP per gene pair, via `np.unique(..., return_index=True)` in file order. This keeps the old `seen` behaviour.
- `blast_to_score` is dropped; the score travels with each hit.

`filter_blocks` still runs when any BLAST line passes. Before, `accepted` was non-empty in exactly that case.

## Testing
Output was compared byte-for-byte against main:

| Dataset | Lifted pairs | Output | Peak RSS main → PR |
| --- | --- | --- | --- |
| Synthetic 1M-line LAST | 36 | identical | 984 → 316 MB |
| Synthetic 1M lines + 30% duplicate anchor HSPs + 8k off-diagonal near-anchor hits (some duplicated) | 8,036 | identical | 1007 → 335 MB |
| Self-self version of the above | 4,762 | identical | — |
| Real `lastal` run (MCscan grape/peach-like) | — | identical | — |

The remaining ~300 MB is the baseline of Python, numpy and the two BED files. The new `test_process_blast_for_liftover` covers dedup to the first HSP, anchor-only `accepted`, and dropping hits on chromosome pairs without anchors.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_019mN8ixeibi7qiB4PzhMo1Y

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37b9752bbed5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.