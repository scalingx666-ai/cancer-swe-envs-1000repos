# Issue

**Title:** Update dependencies

## Description

- [core] [object] Update itertools to 0.15
- [json] Update base64 to 0.23
- [ul] [pixeldata] Update rstest to 0.28
- `cargo update`
- Update Cargo.lock files in fuzz projects

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b232df36c66d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.