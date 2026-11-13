# Issue

**Title:** Fix alias handling for 'lw' and 'linewidth' in patches

## Description

Currently, passing `linewidth` to feature patches (Arrow, Box, etc.) silently fails because a default `lw` is set, and both are passed to Matplotlib, which prioritizes the default `lw`. This update handles `linewidth`  /  `lw` in the same way as  `facecolor` / `fc` are handled in the patches.  

Previously, passing `linewidth=1` in `add_feature()` would still produce a plot without visible edges, only `lw=1` would work. With this fix, both `linewidth` and `lw` will overwrite the default `lw`, ensuring edges are rendered as expected when passing it to a patch.

- Applies to Arrow, Box, RoundBox, Intron, Link in patches.py

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6872f098690`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.