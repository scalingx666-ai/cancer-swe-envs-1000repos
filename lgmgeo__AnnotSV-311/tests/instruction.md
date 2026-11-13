# Issue

**Title:** Revisions for pipeline integration and separate annotations

## Description

This stable PR facilitates adding AnnotSV into custom pipelines as follows:
1. Fixes the base Makefile to allow repeat calls without breaking (i.e. for fast iteration/dumb CLI debugging).
2. Updates template for application.properties to fill phenotype version programmatically (incidental improvement while I was searching the codebase for something else).
3. Modify INSTALL_annotations.sh to download annotation files without relying on the AnnotSV makefile.
4. Added a flag and exposed exomiser-rest-prioritiser path to customize downloads of exomiser/annotation dependencies.

Of note, the variantconvert python install was incidentally found to fail on my setup (docker/alpine) when using system/image-wide installs of python/pip (the -e failed because of externally managed environment). Didn't make a bug report, but happy to do so if desired.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5573d1015c77`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.