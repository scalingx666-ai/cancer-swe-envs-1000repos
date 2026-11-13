# Issue

**Title:** Small fixes to PositroniumSource implementation

## Description

1. Improve the function to recalculate fractions from intensities (second API).
The previous version always assumed that pPs is defined as the first element. The current version should work for any order. Also, the pPs time is set to the value provided by the user; it used some default constant. This function assumes that only one PPs is defined.
3. Remove unused functions from helper
4. Add an error message when handling `PositronElectronInteraction::kParaPsaraPositronium` in `GatePositroniumHelper::CalcFractionsFromLifetime`
5. Improve docs -> Mark that ExtendedVSource is currently obsolete

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7b14976251e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.