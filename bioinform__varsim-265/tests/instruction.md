# Issue

**Title:** Better handling of insertion validation

## Description

- [ ] [RES-XXXX](https://binatechnologies.atlassian.net/browse/RES-XXXX)
- [ ] Blocking PRs: ADD HERE IF ANY
* People
  - [ ] Reviewers (>=1): ADD HERE
  - [ ] Merger (>=1): ADD HERE
  - [ ] FYI: ADD HERE IF ANY
- [ ] Release note (if needed)
- [ ] No code copied from outside Bina 
- [ ] Tests (Unit, Workflow, ITL & Gherkin) are passing
- [ ] PR labels, milestones & assignees

# Summary

* ignore missing or incompatible SVLEN when using `-ignore_ins_len` (for insertion), otherwise ignore variant with missing or incompatible SVLEN
* treat insertions as SVs (so that wiggle can affect interval of the variant) regardless of length when `-ignore_ins_len` used
* added `--ignore_ins_len` to `compare_vcf.py`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f4169a54449`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.