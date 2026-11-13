# Issue

**Title:** Correcting flag documentation in run_inference.py, respectively chang…

## Description

…ing extract_predictions.py

The flag falsely stated that it would disable TTA, however it actually enabled it. Using the extract_predictions.py script as is now will probably result in about 4x faster predictions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88b8e3e2079a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.