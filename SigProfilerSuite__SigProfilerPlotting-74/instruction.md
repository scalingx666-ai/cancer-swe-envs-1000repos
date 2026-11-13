# Issue

**Title:** Give the Interactive Dashboard its own Graphical Interface nav tab

## Description

## Summary

Small docs-only  (merged). Pulls the Interactive Dashboard page out of the "Usage" nav section into its own top-level "Graphical Interface" tab, matching SigProfilerExtractor's docs site layout (`Home | Getting Started | Using The Tool | Output | Graphical Interface`).

Part of the still-unreleased v1.6.0 (no new tag needed for this alone).

## Test plan

- [x] `mkdocs build --strict` passes.
- [x] Verified in a real browser: the "Graphical Interface" tab appears in the top nav and routes to the Interactive Dashboard page.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ed6e8a3737a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.