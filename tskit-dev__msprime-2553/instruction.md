# Issue

**Title:** Fix running airspeed velocity

## Description

Running the latest version of asv gives a strange error message:

```
· Creating environments
· Discovering benchmarks
·· Uninstalling from virtualenv-py3.14-stdpopsim
·· Building 0d2c3be2 <main> for virtualenv-py3.14-stdpopsim..........
·· Installing 0d2c3be2 <main> into virtualenv-py3.14-stdpopsim
·· Last error: Found multiple wheels in f/home/jacob/gsoc/msprime/.asv/env/456be663a40367e1ab355169d2df60ad/asv-build-cache/0d2c3be2a7a0f4f8305d16dce4bf961825f21b8f. Cannot decide correct one
·· Failed to build the project and import the benchmark suite.
```

This is caused by a change to the default build command in asv 0.6.2, so specify an explicit build command similar to the old one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d2c3be2a7a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.