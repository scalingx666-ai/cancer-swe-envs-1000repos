# Issue

**Title:** Plan the next release as a patch release, 6.0.1

## Description

6.0.0 is released, so `nextVersionBump` moves from `"x"` to `"x.x.x"`: master's snapshots become `6.0.1-<hash>-SNAPSHOT` rather than `7.0.0-<hash>-SNAPSHOT`.

- Checked with `./gradlew printVersion`: `6.0.1-0d106fb-SNAPSHOT`.
- No CHANGELOG entry: build configuration only.

@coderabbitai ignore

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d106fb9b3eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.