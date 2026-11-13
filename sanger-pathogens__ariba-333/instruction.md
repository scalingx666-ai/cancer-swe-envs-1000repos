# Issue

**Title:** Use GitHub actions for tests and builds

## Description

Changes:
* Remove travis build
* Add Singularity definition file, and change Dockerfile and install dependencies script so that singularity and docker builds both use the install dependencies script
* Add github actions workflow. It builds the singularity container and runs the tests inside it.
* Update README  - badges changed (some no longer relevant) and added/updated singularity/docker instructions

The new workflow runs on push to master or on pull request. If a tag is pushed (in the form `v*.*.*`) then the workflow additionally makes a new github release, uploads the singularity container to the release, and builds the docker container and adds it to github container registry.

Release process successfully tested on my fork of the repo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd739aaea245`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.