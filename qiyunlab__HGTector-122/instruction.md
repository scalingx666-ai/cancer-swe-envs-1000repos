# Issue

**Title:** overcommit + relax blast threads

## Description

1) Overcommit: os.cpu_count() returns the number of physical cores available on the computer it runs on. BUT this is not the number of AVAILABLE cores for the running process.
eg in slurm allocation, you can run on a node with 96 cores, but only have access to n cores regarding the allocation.
see:
```
# Standard slurm allocation -> 1 core
maestro-submit:~ > srun python3  -c "import os; print(os.cpu_count(),  len(os.sched_getaffinity(0)))"
96 1
```
same can be checked with taskset
```
taskset -c 0 python3  -c "import os; print(os.cpu_count(),  len(os.sched_getaffinity(0)))"
96 1
```
2) blast thread limit.
blast+ is NOT limited to 8 threads, relax this hardcoded value and use num_threa
ds according to what was requested AND available ones

regards
Eric

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d4e8a139a10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.