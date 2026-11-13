# Issue

**Title:** fix: :bug: Improving cell detection performance, fixed bugs, extendin…

## Description

…g documentation, add mixed precision

Improving runtime for inference by using an improved structure. Postprocessing of cell detection is speed up by a factor of x100. Also fixed a small bug regarding double cell entries in the overlap area. Adding mixed precision as optional training option. Adding more documentation

Double cell detection in cell_detection.py and speed is increased by a large margin

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `babc0a2a83bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.