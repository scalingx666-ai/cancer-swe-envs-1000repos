# Issue

**Title:** Update numpy/pandas usage for pandas 3.x and numpy >=2.4

## Description

Hi Kez,

A handful of small changes to get things compatible with latest pandas and numpy

Small updates to dysgu to be compatible with NumPy 2.4.1 and Pandas 3.0.0 while 
maintaining backwards compatibility. The notable change for each package was:
- Numpy >=2.4 no longer supports single-valued arrays to scalar conversions
- Pandas 3 no longer treats empty as `''` but instead `NaN`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `285f234efacc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.