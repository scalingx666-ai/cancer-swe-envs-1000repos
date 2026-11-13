# Issue

**Title:** Add a docker renv layer to speed up build time

## Description

## Issue Number

N/A

## Purpose/Implementation Notes

This pull request introduces a major refactor of the Docker build pipeline to use content-addressed (content-hashed) intermediate images for all worker R environments. This change improves build caching, reproducibility, and efficiency by ensuring that only the relevant layers are rebuilt when dependencies change. The refactor also splits out the creation of worker R environments into dedicated `*_r_env` images, which are then used as the base for their respective worker images.

The most important changes are:

**Docker build pipeline refactor and content-addressed images:**

* Refactored `docker-bake.hcl` to define new variables and functions for content-addressed tags, and added new targets for each worker's R environment (e.g., `smasher_r_env`, `illumina_r_env`, etc.), which are tagged by the content hash of their dependencies. Downstream worker images now use these as their base, improving cache efficiency and reproducibility. [[1]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2R33-R55) [[2]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2R123-R139) [[3]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2R247-R333) [[4]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2L229-R363) [[5]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2L247-R373) [[6]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2L257-R384) [[7]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2R438-R450)

* Updated the main worker Dockerfiles (e.g., `Dockerfile.smasher`, `Dockerfile.illumina`, etc.) to use their corresponding `*_r_env` images as the base, passing in the appropriate content hash as a build argument. The R dependency installation steps were moved out of these Dockerfiles and into the new `*_r_env` images. [[1]](diffhunk://#diff-b84707d387a9bc6ce71be5d192edfa5a0fa11ba1daf6699332119fc8a40e293bL2-L14) [[2]](diffhunk://#diff-9c9544798b66a8ddfae57fa22b9afcb39cfc20f5d66c9c11db0cd99064f8d84cL2-L14) [[3]](diffhunk://#diff-858ed3fe3532afecf47ed68716c2e99a4ed335d0633025ed253c68fe3767bf10L2-L14) [[4]](diffhunk://#diff-8eae0928dfd7b519ba5cd8096d44070c3c2b205d22fdc1d517ed4360981ed848L2-L14) [[5]](diffhunk://#diff-85f55659baa2e8b16d8518d8fa331c9e32e97cd16c0471d9ec4ae9ab156ebb5fL2-L14) [[6]](diffhunk://#diff-29d25019d22c78c05a9fc64a5e2aaa55283391b6a80c71e585a0889556d1bd02L5-L17) [[7]](diffhunk://#diff-255e4d8d511860e8b06d8e39bd5bfafc2f5790889feae5e4152810713b2c9a11L2-L17)

**New intermediate R environment images:**

* Added new Dockerfiles `Dockerfile.r_env` and `Dockerfile.affymetrix_r_env` to build the content-addressed R environments for each worker. These Dockerfiles handle installing R dependencies based on the appropriate `renv.lock` files. [[1]](diffhunk://#diff-7cc7e6d1552fc506370f4407ff7baffeb43e13e3418b83162a4a2c613a626005R1-R15) [[2]](diffhunk://#diff-929846bdd0aff6904e64156e633603de5c92141be50b1e47686c2fcb6721a258R1-R17)

**Base image improvements:**

* Modified `common/dockerfiles/Dockerfile.base` to support content-addressed references by using an `UBUNTU_DIGEST` build argument, ensuring the base Ubuntu image is pinned by digest for reproducibility.

**Build group updates:**

* Updated the `all` group in `docker-bake.hcl` to include all new `*_r_env` intermediate targets, ensuring they are built and pushed as part of the standard build pipeline. [[1]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2L300-R427) [[2]](diffhunk://#diff-870f6fe23fc034f008f5203ee1e628d7bfa65a49095d5a4688db498328449ed2R438-R450)

These changes significantly improve Docker layer caching and image reproducibility, reducing unnecessary rebuilds and making image builds more deterministic.

## Types of changes

- Bugfix (non-breaking change which fixes an issue)
- New feature (non-breaking change which adds functionality)

## Functional tests

N/A Tested building locally

## Checklist

- [x] Lint and unit tests pass locally with my changes

## Screenshots

N/A

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cfe10ff8700d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.