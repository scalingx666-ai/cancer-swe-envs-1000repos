# Issue

**Title:** Upgrade libbrotli1 via apt in baseimage (CVE-2026-111497)

## Description

## Summary

Adds `libbrotli1` to the existing `apt-get upgrade -y` list in the baseimage so the Ubuntu 26.04 security update (1.2.0-3ubuntu0.1) is installed. This addresses 1 CVE.

## Closes

## Per-CVE rationale

### [CVE-2026-111497] (#1142)
- **Fix:** add `libbrotli1` to the `apt-get upgrade -y ...` line in `docker/Dockerfile.baseimage` (FixedVersion 1.2.0-3ubuntu0.1 per trivy-results.json)
- **Precedent:** 423d1625 — "upgrade gpgv via apt" added `apt-get upgrade -y gpgv` to the baseimage RUN block; later extended with openssl/curl packages in the same line
- **Confidence:** dockerfile-precedent
- **Availability:** Ubuntu OS package (fix_shape `os-package`); not a conda pin
- **Coupled bumps:** none
- **Maintainer guidance:** none

## Files changed

- `docker/Dockerfile.baseimage` — add `libbrotli1` to the apt upgrade list

---

*This PR was authored by Claude Sonnet 5.5 (running on Google Vertex
AI via the `container-scan.yml` auto-fix pipeline). Review every
file change, every cited commit SHA, and every justification before
merging. The CI Trivy scan must pass before merge.*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0c73733303f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.