# Issue

**Title:** Kerpedji/cross section fix

## Description

## Description

> What was changed in this pull request?

Horizontal and vertical cross sections were broken on tilesets that provided resolutions rather than just zoom levels. This PR fixes that.

> Why is it necessary?

Fixes #___

## Checklist

- [ ] Set proper GitHub labels (e.g. v1.6+, ignore if you don't know)
- [ ] Unit tests added or updated
- [ ] Documentation added or updated
- [ ] Example(s) added or updated
- [ ] Update schema.json if there are changes to the viewconf JSON structure format
- [ ] Screenshot for visual changes (e.g. new tracks or UI changes)
- [ ] Updated CHANGELOG.md

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2dcd2190180b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.