# Issue

**Title:** Fix PyPI publishing metadata and authentication

## Description

The 0.1.6 distributions pass the current Twine check, but publishing fails because the old v1.8.14 action cannot read Metadata-Version 2.4 and incorrectly reports missing Name/Version. The workflow also passes an account username/password, which PyPI no longer accepts.

Update the publishing action to v1.14.3 (pinned to its verified commit), remove legacy password authentication, and use PyPI Trusted Publishing in a separate job with job-scoped `id-token: write`. Build and validate distributions on pull requests; publishing remains manual and is restricted to `master` and the `pypi` environment.

`RELEASING.md` documents the one-time PyPI Trusted Publisher setup: owner `pyranges`, repository `pyranges0`, workflow `build_and_upload_wheels.yml`, environment `pypi`. This must be registered on PyPI before the first publishing run. Start a new workflow run after merging rather than rerunning the old failed run.

Validation:
- Downloaded the failed run's artifacts and confirmed their Name/Version fields are present with metadata 2.4.
- Reproduced the missing-field result using the older pkginfo reader.
- Both original distributions and freshly rebuilt wheel/sdist pass `twine check --strict` with Twine 7.0.0.
- Workflow YAML parsing and `git diff --check` pass.
- No package upload was attempted; version remains 0.1.6.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d20e8282925`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.