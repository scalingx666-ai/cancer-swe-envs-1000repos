# Issue

**Title:** Update Dockerfile

## Description

I ran into this error running the docker build today (docker 20.10.11)

```
Step 4/10 : COPY setup.py README.md /opt/truvari-source
When using COPY with more than one source file, the destination must be a directory and end with a /
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `907f6ef95757`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.