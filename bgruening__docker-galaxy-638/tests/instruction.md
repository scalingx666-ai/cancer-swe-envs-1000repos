# Issue

**Title:** Build the Galaxy 26.1 image with HTCondor and ARM64 support

## Description

Supersedes #633.

This rebases the HTCondor runner migration onto #634 (which is based on #635), giving us one integration branch for the modern Galaxy 26.1 appliance.

Changes carried forward from #633:
- install the htcondor Python distribution used by Galaxy’s htcondor2 runner
- configure galaxy.jobs.runners.htcondor:HTCondorJobRunner
- expose GALAXY_RUNNERS_ENABLE_HTCONDOR
- update Flower to 2.0.1

The temporary Galaxy fork/reference from #633 is intentionally not retained: official Galaxy release_26.1 now contains the HTCondor runner.

This also inherits #634’s multi-architecture image build and ARM64 boot/readiness smoke test. Please merge #635, then #634, before this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a704596b4a73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.