# Issue

**Title:** docs: move to scverse-doc and adopt the shared scverse docs TOC

## Description

#### Reference Issue or PRs

scverse/scverse-doc#62

#### What does your PR implement? Be specific.

Switches the docs from the scanpydoc theme to scverse-doc and groups the sidebar into Getting started, Guides, Reference and Project as agreed in scverse/scverse-doc#62, with the minimal pipeline example as the quickstart.
The logo greens are set in conf.py until scverse/scverse.github.io#381 and a scverse-doc release put them in the registry.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ca3b74c9b2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.