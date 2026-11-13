# Issue

**Title:** Consolidate dot_prep into uniq_anchor; add regression tests

## Description

## From Maria

Remove a duplicate step that Dot and Assemblytics had in common. They both did unique anchor filtering, so now that's only done once.
Also add pytest with a github action to ensure basic regression testing runs automatically on all new PRs.

## From Claude

- **Eliminates duplicate delta reads**: `dot_prep.py` previously re-read the delta file twice and re-ran the full planesweep filtering that `uniq_anchor.py` had already done. Now `uniq_anchor.run()` builds and returns `(reference_lengths, fields_by_query)` during its existing second pass, which `cli.py` threads directly into `index_for_dot()`.
- **-281 lines of duplicate code** removed from `dot_prep.py` (duplicate `summarize_planesweep`, `binary_search`, `getQueryRefCombinations`, `calculateUniqueness`, `writeFilteredDeltaFile`).
- **~3-5s faster** per run (Drosophila: 16s → 12.6s, Human: 39s → 34s).
- **Fixed a latent bug** in `index_for_dot()` where `all_references_by_query` used a stale `ref` variable for repetitive alignments instead of `fields[6]`.
- **Regression tests**: new `tests/test_pipeline.py` runs the full pipeline on the ecoli example (~5s) and does exact-match comparison against checked-in fixture files for all key text outputs.
- **CI workflow**: `.github/workflows/test.yml` runs `pytest` on every push and PR.

## Test plan
- [ ] CI passes (test workflow runs on this PR)
- [ ] Load ecoli/drosophila/human delta in web app Dot tab and confirm visualization renders correctly

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5d824f029c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.