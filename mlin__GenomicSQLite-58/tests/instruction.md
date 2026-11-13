# Issue

**Title:** Rust: check in Cargo.toml with a literal version

## Description

Check in literal Cargo manifests and remove both cargo wrappers and manifest templates. CI, CMake, and Docker now call cargo directly.

Previously, wrapper-generated manifests depended on locally available tags, so agreement with the committed lock varied by checkout. The v0.10.0 lock refresh required special tag handling in CI.

The git tag remains the version source for all five release artifacts. The Rust crate's checked-in version and lock root are `0.0.0`. Publishing stamps the tag's version into the publish checkout without requiring a version commit. The committed `Cargo.lock` continues to pin dependencies.

The standalone smoke crate's pin is also a dummy (`=0.0.0`). The release-smoke workflow rewrites that pin to the version under test in its disposable checkout.

Verified locally: the Rust 1.75 floor passes with the committed lock; the ceiling passes after updating rusqlite to the newest allowed version. A publish-stamp simulation (`0.0.0` → `0.10.1`) changed only the lock's root version, preserved all dependency pins, and packaged successfully.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ebd132ff7c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.