# Issue

**Title:** y-axis transformation bug

## Description

Hi, really like the package!

Was getting this error when using log2 or log10 for scale.intersections:

Error in seq.default(min, max, by = by) :
  'from' cannot be NA, NaN or infinite

Traceback showed it was a ggplot issue
Replacing 0 with NA for minimum limit as recommended here:
solved my issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `731cb87755a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.