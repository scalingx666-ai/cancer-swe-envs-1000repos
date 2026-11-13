# Issue

**Title:** Clarify that Staging publishes to Maven Central and Production to PyPI

## Description

## Summary

After splitting the release into a Maven Central workflow and a PyPI workflow, the GitHub **environment** names are misleading:
- `Staging` now holds the **Maven Central** publishing secrets (Sonatype token + GPG key).
- `Production` now does the **PyPI** publish (OIDC trusted publishing).

Rather than *rename* the environments — which would require re-entering the GPG key and reconfiguring the PyPI trusted-publisher — this documents the mapping where it's needed:

- A `NOTE` comment at each workflow's `environment:` line.
- A mapping table at the top of `RELEASE.md`.

## Mapping

| Workflow | File | Environment | Publishes to |
|---|---|---|---|
| Publish to Maven Central | `staging-release.yml` | `Staging` | Maven Central |
| Publish to PyPI | `production-release.yml` | `Production` | PyPI |

Docs/comments only — no behavior change.

---
This pull request and its description were written by Isaac.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33701574c3ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.