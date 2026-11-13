# Issue

**Title:** Fix vg pack undercounting coverage from GAF

## Description

. Probably also the cause of #3546.

## Problem

`vg pack -a` (GAF input, without `-e`) has undercounted coverage since v1.35.0. For long reads it counts almost nothing; for short reads with errors it counts about half.

`pack` reads GAF without looking up matched bases in the graph, which is faster, so each alignment's sequence holds only its mismatched and inserted bases. `Packer::add` took the read length from that sequence to place the read-end cutoff for `--trim-ends`. It then counted only matched bases at read positions below k, the number of mismatched and inserted bases, even when trimming was off. Reads that matched the graph exactly had an empty sequence, the cutoff underflowed to `SIZE_MAX`, and they were counted in full, which hid the bug.

## Fix

`Packer::add` now measures the read along its path, the same positions that `position_in_read` counts, and never reads the sequence. For a GAM alignment the two lengths are equal. The cutoff is now an exclusive end, so it cannot underflow.

## Tests

`test/t/34_vg_pack.t` already compared GAF and GAM packs, but it simulated error-free reads, so the comparisons passed trivially. It now simulates substitutions and insertions (`vg sim -e 0.01 -i 0.002`). It also compares GAF and GAM with read ends trimmed (`-s 5`), for nodes and for edges.

- On the unfixed binary, the four GAF-vs-GAM tests fail and the other 18 pass.
- With the fix, all 22 pass. `t/18_vg_call.t`, `t/49_vg_depth.t` and `t/41_vg_viz.t` also pass.
- On 500 simulated 150 bp reads at 1% error, total base coverage was 74,281 from GAM and 18,408 from GAF before the fix. After it, GAM, GAF, and GAF with `-e` all give 74,281.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9cf5f55c0617`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.