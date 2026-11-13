# Issue

**Title:** Fix bug of usage of OR keyword of query

## Description

## Description
<!-- Add a more detailed description of the changes if needed. -->
Now, topic's keyword looks like `SLAMOR"Visual Odometry"`.
However, it should be `SLAM OR "Visual Odometry"` according to [document of python lib](https://lukasschwab.me/arxiv.py/arxiv.html#Search.query).
In fact, we are getting wrong results now.

## Related Issue
<!-- If your PR refers to a related issue, link it here. -->
There is no related issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6a4e2fc4662`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.