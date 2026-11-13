# Issue

**Title:** [FIX] ProSE: an RT chunk of mostly false calibration PSMs takes the precursor offset of its neighbours

## Description

## Description

. With `calibration:recalibrate`, a retention-time chunk of the precursor model where most of the calibration PSMs are false matches no longer takes their median. Instead it takes the model of its neighbours. The chunks are told apart by the decoy hits among the calibration PSMs. Runs without such a chunk are bit-identical to develop.

**Problem.** The precursor model is the median error of the calibration PSMs per RT chunk (10 by default), interpolated between the chunks. When most of a chunk's PSMs are false matches, the median is theirs, and it need not be near the instrument's error.

On a PXD019643 class I immunopeptidomics run, a contaminant elutes over the last third of the gradient: a precursor series 22.013 m/z apart, i.e. PEG 2+. It is matched to targets and decoys alike, at a systematic +10 to +13 ppm. So the last three of eight chunks got +8.9 to +10.7 ppm. The correct PSMs there, as MSFragger + Percolator accept them, are at 0.04–0.21 ppm. After the correction, they were outside the ±5 ppm search window.

| chunk (RT, s) | 1687 | 2387 | 2872 | 3349 | 3987 | 4488 | 4992 | 5517 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| estimated false share (2 × decoys / n) | 0.48 | 0.33 | 0.59 | 0.37 | 0.52 | 0.78 | 0.96 | 0.85 |
| chunk median, develop (ppm) | −0.41 | 0.25 | 0.25 | 0.13 | 0.52 | 9.91 | 10.72 | 8.92 |
| MSFragger accepted PSMs (ppm) | −0.34 | −0.47 | 0.16 | 0.05 | 0.14 | 0.21 | 0.21 | 0.04 |

**Change.**
- The calibration pass marks each calibration PSM whose best hit is a peptide of a decoy protein. It uses the decoy marker the search already determined (`decoy_string`, prefix or suffix).
- `MzRecalibration_::fit()` takes these flags (optional, default none) and counts the decoys per chunk.
- A chunk where more than a quarter of the PSMs are decoy hits has an estimated majority of false matches (as many false targets as decoys, so twice the decoys). That is past the breakdown point of the median, so such a chunk takes the model of its neighbours:
  - inside the run: interpolated at its RT between the nearest reliable chunks before and after it, as the model interpolates between chunks;
  - at the ends of the run: the model of the nearest reliable chunk;
  - when no chunk is reliable: the median of all points, one offset for the run.
- Such a chunk is marked `from_neighbours`. The model string in the log, the search parameters and the run summary shows it as `(<points>, <decoys> decoys: mostly false matches)`, and an INFO line counts these chunks.
- Only the precursor model uses the flags; the fragment models are unchanged. A false match repeats its precursor error (the same PEG ion next to the same peptide mass), but the fragment peaks it explains are random peaks across the fragment window, whose median stays near 0. On PXD019643 the fragment chunks of the three PEG chunks are at −0.4, −1.5 and −0.3 mDa, at most 7.5% of the 0.02 Da tolerance.
- The documentation of `calibration:recalibrate` and the calibration note of the ProSE tool are updated.

**Design rationale.**
- A drift of the instrument shifts the errors of correct PSMs and must still be followed. The last chunk of a PXD011695 EThcD run is at −14.7 ppm; MSFragger accepts PSMs of 77 distinct peptide/charge combinations there, at a median of −18 ppm. That chunk has 1 decoy among its 88 PSMs, so it is fitted as before. A false contaminant is matched to decoys as often as to targets; a drift is not.
- Two alternatives were tested and dropped:
  - Fitting each chunk within the core of the run's errors (the fix first proposed in #10885) excluded the drifted PSMs of the EThcD run: −235 PSMs (−1.8%).
  - Counting each theoretical precursor m/z once fixed PXD019643 only in part. Different false peptides are matched to the same PEG ion, so the late chunks stayed at 5.2 and 8.6 ppm.
- The threshold is the breakdown point of the median, not a tuned value. In the six tryptic runs whose calibration PSMs I dumped (iPRG2015, HFX, Astral 250 pg, Velos, Lumos TMT, PXD011695 EThcD), no chunk exceeds an estimated false share of 0.32. In the two immunopeptidomics runs the flagged chunks are at 0.53–0.96.

**Effect** (PSMs / peptides at 1% FDR, the 11 runs of the ProSE benchmark pilot):

| Run | develop | this PR |
|---|---|---|
| PXD019643 class I | 2,967 / 1,058 | 3,621 / 1,297 (+22% / +23%) |
| PXD058436 class I (timsTOF) | 10,575 / 6,571 | 10,446 / 6,606 (−1.2% / +0.5%) |
| PXD011695 EThcD, iPRG2015, HFX, Astral 250 pg, Lumos TMT, Eclipse TMTpro, PXD065289, Lumos CID, Velos | | bit-identical |

- On PXD019643, five of eight chunks take the model of their neighbours, and the last three are now at 0.13 ppm. MSFragger reaches 4,148 / 1,481 on the same run.
- On PXD058436, every chunk is flagged (estimated false share 0.53–0.85), so the run gets one offset of 1.40 ppm. Per chunk, it is 0.32 ppm on average from the median of MSFragger's accepted PSMs (at most 1.08). The chunk medians of develop were 0.65 ppm away on average (at most 1.34). The counts change within the run-to-run noise of about ±1%.

**Tests.**
- `ProSEAlgorithm_test` has new tests of `MzRecalibration_::fit()` with decoy flags:
  - chunks of false matches at the end of a run take the model of the last reliable chunk, with and without `linear`;
  - a chunk inside the run takes the model interpolated between its neighbours, while a −18 ppm drift with one decoy is followed;
  - when every chunk is flagged, all chunks get the median of all points;
  - flags that flag no chunk change nothing;
  - a flag vector of the wrong size gives an inactive model.
- Debug build: `ProSEAlgorithm_test` passes.
- Release build: `ctest -R ProSE -E ProSEAlgorithm_test` passes 251 of 251 (TOPP, INI and CTD tests).

**Context.** This came up in the pilot of the ProSE paper benchmark. This PR does not change the tag `prose-benchmark-2026-11`.

## Checklist
- [x] Make sure that you are listed in the AUTHORS file
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] New and existing unit tests pass locally with my changes
- [x] Updated or added python bindings for changed or new classes (Tick if no updates were necessary.)

### AI use (see the [OpenMS AI Policy](https://openms.de/ai-policy/))
- [x] I have read the [OpenMS AI Policy](https://openms.de/ai-policy/), and I understand, have reviewed and tested every change in this PR and can explain it in my own words
- AI use in this PR (tick one):
  - [ ] None
  - [ ] Assisted (e.g. completion, suggestions, small edits); commits carry an `Assisted-by:` trailer
  - [x] Substantial (e.g. agentic tools wrote significant parts); commits carry a `Co-authored-by:` trailer, and the description above explains the design intent and rationale

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved precursor mass recalibration when a time-range chunk contains more than 25% decoy matches: it now uses a model from reliable neighboring chunks. If all chunks are affected, calibration uses a run-wide median offset.
  * Reliable chunks retain their own calibration models, including when they reflect genuine instrument drift.

* **Documentation**
  * Clarified how decoy-heavy calibration chunks are handled.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82f99f83c892`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.