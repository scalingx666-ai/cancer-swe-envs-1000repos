# Issue

**Title:** automation: adding `dependabot` for github actions

## Description

Dependabot itself already implements the functionality to keep GitHub actions up to date.

This PR implements a minimal viable dependabot workflow to update:
- Github Actions only
- on a weekly basis
- pointing the PR to our dev branch `rubicon`
- Call the commit message `Github Actions: <<action updated>>`

Optinally, we may want to `labels` to the workflow to add labels to the PR (we'd have to add these to the repo) 
```
    labels:
      - "dependencies"
      - "github-actions"
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d90a774b00f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.