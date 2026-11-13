# Issue

**Title:** remove_indexes_h5.py fix: move break logic to start of loop.

## Description

Before fix, since `index` is updated at the end of the loop after checking the stop condition, `index` is incremented past `num_tiles` and gives an IndexError in next iteration.

Since the error happens after all retained items are copied over, it seems it doesn't cause issues, but the error message can still be misleading or lead to issues in the future if subsequent logic is added.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a62f1178c8dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.