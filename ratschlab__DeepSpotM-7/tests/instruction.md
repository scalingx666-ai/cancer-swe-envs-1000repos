# Issue

**Title:** docs: use the paper's own abstract in CITATION.cff

## Description

The `abstract` field added in #5 was a paraphrase I wrote from the README, not the preprint's abstract. This replaces it with the published text.

It matters because `CITATION.cff` is what GitHub's *Cite this repository* box, Zenodo and citation managers read — a paraphrase there quietly becomes the project's description wherever the file is consumed.

The software-specific note (PolyForm Noncommercial for code, CC-BY-NC-SA-4.0 for weights, research use only) is kept as a short trailing sentence, since the paper abstract does not cover licensing.

Verified: `CITATION.cff` still validates against cff-version 1.2.0 (`cffconvert`), and the abstract round-trips through the YAML folded scalar verbatim.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `429fa2ecdc59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.