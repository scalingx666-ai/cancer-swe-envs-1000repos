# Issue

**Title:** Add mTRE measured in world coordinate frame

## Description

.

`pose` maps camera coordinates to CT coordinates, so mTRE now applies `pose.inverse()` to the fiducials, as `perspective_projection` does. This measures the error at the fiducials instead of near the X-ray source.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `caa55cc80962`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.