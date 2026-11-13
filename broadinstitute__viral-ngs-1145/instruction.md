# Issue

**Title:** Upgrade apt and libapt-pkg7.0 via apt in baseimage (CVE-2026-109518)

## Description

## Summary

Adds `apt` and `libapt-pkg7.0` to the existing `apt-get upgrade -y` list in `docker/Dockerfile.baseimage`, pulling in Ubuntu's fixed 3.2.1ubuntu0.1. This addresses 1 open CVE issue.

## Closes

## Per-CVE rationale

### [CVE-2026-109518] (#1144)
- **Fix:** add `apt libapt-pkg7.0` to the `apt-get upgrade -y` list in docker/Dockerfile.baseimage
- **Precedent:** 2823b591 — added libbrotli1 to the same upgrade list (CVE-2026-111497); verified with git show
- **Confidence:** dockerfile-precedent
- **Availability:** Ubuntu OS package, FixedVersion 3.2.1ubuntu0.1 per trivy-results.json; not a conda package (fix_shape os-package)
- **Coupled bumps:** none
- **Maintainer guidance:** none

## Files changed

- `docker/Dockerfile.baseimage` — append `apt libapt-pkg7.0` to the apt-get upgrade list

---

*This PR was authored by Claude Sonnet 5.5 (running on Google Vertex
AI via the `container-scan.yml` auto-fix pipeline). Review every
file change, every cited commit SHA, and every justification before
merging. The CI Trivy scan must pass before merge.*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfc4265c502f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.