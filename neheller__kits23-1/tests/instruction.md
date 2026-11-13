# Issue

**Title:** metrics, ranking and segmentations as uint8

## Description

# metrics, ranking and segmentations as uint8

## Description
Added metrics and ranking with minor modifications/simplifications from kits21. 
Modifications include own implementation of Dice, removal of sampling (not needed for 23) and code restructuring.

Made segmentations uint8 because there is no need for int32 with 4 labels (waste of RAM) 

Added documentation (located in kits23.evaluation) for how to run evaluation and ranking


## Checklist

- [x] Merged latest `master`
- [there is no version number] Updated version number in `README.md`
- [this file does not exist] Added changes to `changelog.md`
- [x] Updated version number in `setup.py`
- [x - but why do we need this file? kits23.__version__ will give the version defined in setup.py. There is no need to have this in addition] Version number in `kits23/_version.py` matches `setup.py`
- [ ] (only when updating dataset) Ran `annotation.import` to completion

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2699006dac3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.