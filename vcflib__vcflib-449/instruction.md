# Issue

**Title:** Parallelize vcfwave across records with -t

## Description

On my test data the new `-t` parallelism gives a nearly linear speedup, even beyond 20 cores.  

Whereas the old logic (formerly `-t`, now `-w`) would often lead to a slow-down after 2 or 3 cores.

Keeping the old logic (under the new `-w` name) around in case there's a use case for it that's not covered by what I'm testing on...

Also, I looked at combining `-t` and `-w` but wasn't able to get a useful speedup to justify the added complexity of nested threading....

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b118a9bfd99b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.