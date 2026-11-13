# Issue

**Title:** fix run summary duplication rate, rank curve and labels

## Description

, from a second review of the run summary and the visualizer.

## UMI duplication rate over barcoded reads only

The rate was `(Total assignments processed - Total reads saved) / Total assignments processed`, but "Total assignments processed" also holds reads without a barcode, which never enter deduplication — so they were counted as PCR duplicates and the rate was inflated by the unbarcoded share. It is now computed over "Assigned to any gene and barcoded", exactly the reads that are deduplicated. The JSON and the HTML now share one property (`RunSummary.umi_duplication_rate`) instead of two copies of the formula. Note the 55.7% Visium HD figure quoted in #428 used the old formula.

## Rank curve always ends at the last group

`10 ** log10(n)` rounds below `n` for many sizes (401 among them), so the subsampled barcode rank curve ended one rank short. The last rank is now always included, still at most 400 points.

## Labels that say what is counted

The summary now knows whether reads were split into molecules (`--split_molecules`) and whether UMI deduplication ran, from the run's settings rather than from files on disk:

- "Input reads" reads "Input molecules" when reads were split before mapping, and "Reads/Molecules on processed references" when some references were not processed; the mapping rate is labelled "(processed references)" in that case.
- In single-cell/spatial modes counted reads are labelled "after UMI deduplication"; the "share of …" rows follow the same wording.
- Both flags are also written to `SAMPLE.summary_stats.json`.

## Docs

- `--read_group_strategy` takes the strategy name used in the grouped counts file names (`tag_CB`, `file0_col1`, …), not the `--read_group` value. Its default follows the user's `--read_group` order; strategies IsoQuant adds on its own are not saved in `.params`, so for them the alphabetically first one is used.
- An unknown `--read_group_strategy`, a missing GTF or a wrong output directory now print `Error: ...` instead of a traceback.
- `--no_report` is documented in `docs/cmd.md`; `docs/output.md` defines input reads/molecules, reads on processed references, counts after UMI deduplication and the duplication rate.
- Comments no longer claim `--keep_tmp` keeps per-chromosome files: merging removes them, only a crashed or interrupted run leaves them behind.

## Testing

- New/updated tests in `isoquant_tests/test_run_summary.py`: duplication rate over barcoded reads, the rank curve's last point for every size from 401 to 4999, and the split-molecules / UMI / partial-input labels.
- Unit tests not run locally (project convention); CI will run them on this PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e508a04eea0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.