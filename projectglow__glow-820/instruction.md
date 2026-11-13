# Issue

**Title:** Split release into a Maven Central workflow and a PyPI workflow

## Description

## Summary

With the move to the native Central Portal flow, the two release workflows had drifted into a muddle — `staging-release` did **Maven Central + Test PyPI**, and `production-release` did **real PyPI + a now-dead Scala-promote job**. This splits them so each does one thing:

| File | New name | Does |
|---|---|---|
| `staging-release.yml` | **Publish to Maven Central** | `publishSigned` + `sonatypeCentralRelease`, test the staged artifact, build + upload the assembly (fat) jar |
| `production-release.yml` | **Publish to PyPI** | build the wheel (`python setup.py bdist_wheel sdist`) + publish `glow.py` to PyPI |

## Details

**`staging-release.yml` (Maven Central):**
- Removed the Python wheel build, the Test PyPI push, and the conda / `Install correct PySpark version` steps they required (the Scala publish + `stagedRelease/test` + `core/assembly` don't need them).
- Kept the assembly (fat) jar build + upload — it's a Scala/Java artifact.
- Fixed the stale `scala-version` hint (`2.13.14` → `2.13.15`).

**`production-release.yml` (PyPI):**
- Removed the obsolete `push-scala` / `sonatypePromote` job (Scala is published by the Maven workflow now) and the unused `java-version` input.
- Corrected the `push-python` description (real PyPI, not Test PyPI).

## Supersedes
- **#818** — its `bin/build` → wheel-build fix is moot here; the wheel build now lives only in the PyPI workflow (which already builds it correctly).
- **#819** — folded into this PR.

---
This pull request and its description were written by Isaac.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d59eca17c0cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.