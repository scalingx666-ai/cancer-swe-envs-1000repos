# Issue

**Title:** Multiprocessing for GRN

## Description

Major fixes:
* Switched to multiprocessing for GRN step
* Added a test profile to quickly test the pipeline
* Default container is now `aertslab/pyscenic:0.9.19`

Minor fixes:
* Allow a seed to be set (only applied to the GRN step)
* When using Singularity, the image is now always pulled from DockerHub
* Updated requirements file to match pySCENIC
* Code cleanup

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56229aace162`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.