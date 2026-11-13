# Issue

**Title:** NickAkhmetov/fix #1300: update external dependencies in build script to include React JSX runtimes

## Description

## Description

> What was changed in this pull request?

This PR adds the react jsx runtime and jsx dev runtime to the externalized libraries.

> Why is it necessary?

The bundled runtimes otherwise cause Higlass to crash when embedded in React 19 sites.



## Checklist

- [x] Set proper GitHub labels (e.g. v1.6+, ignore if you don't know)
- [x] Unit tests added or updated
- [x] Documentation added or updated
- [x] Example(s) added or updated
- [x] Update schema.json if there are changes to the viewconf JSON structure format
- [x] Screenshot for visual changes (e.g. new tracks or UI changes)
- [x] Updated CHANGELOG.md

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `108656344b01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.