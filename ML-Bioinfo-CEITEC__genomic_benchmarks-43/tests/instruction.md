# Issue

**Title:** added functionality for excluding genomic regions that contain Ns

## Description

- I added functionality for including only genomic regions that do not contains 'N' in the Utils for random generation code cell. For now I kept everything else as is, I did not return the sequence as well but this can easily be added. 
- I also moved the numpy set seed to be included per cell because repetitive execution of cells will consume random numbers if set only at the beginning. The seed set per cell ensures the output of the cell is always the same (even no matter how many times you run the same cell). 
- Ran notebook successfully to the end. 
- Also pushed new datasets.

Note:
The cells that load the genomic references assume that references have already been downloaded in the cache location. Do we want to add a download if does not exist code cell before this?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `605d8539830e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.