# Issue

**Title:** [cudaaligner] myers_gpu uses workspace per block now

## Description

* aligner_global_banded_myers launches thread-blocks depending on the SM count of the GPU.
* Each thread-block has its own workspace and processes multiple alignment tasks sequentially.
* There are two different workspace sizes: n large workspaces for the n largest alignments, many "small" workspaces.

This allows to compute more alignments in a batch due to reduced memory usage per alignment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9fd82325b546`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.