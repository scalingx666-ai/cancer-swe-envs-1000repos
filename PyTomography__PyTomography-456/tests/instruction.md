# Issue

**Title:** Proton CT tutorial: all 188.6 million protons

## Description

The proton CT tutorial now reconstructs every proton of the scan instead of a quarter of them.

## Changes

- **Dataset registry:** `PCT/GATE-Abdomen330-DTC` downloads the full file, `abdomen330_spot_likely.h5` (188.6 million protons, 7.5 GB). The quarter file (1.9 GB) stays in the same Zenodo record, 23815070. Zenodo serves the full file at the pinned size and checksum.
- **Tutorial text:** `t_pct_abdomen` reads the full file. It says how to read a quarter with less memory (`io.PCT.load_listmode(..., fraction=0.25)`), and gives the new memory and time.
- **Outputs:** from a run on 4.0.0, written back with `run_tutorials.py --write-back`.
- **Viewer images:** uploaded to PyTomography/Tutorial-Images under `v4.0.0/`, commit 23e47592, and pinned in `viewer_images.json`. Only this tutorial's images changed.
- **Script:** `examples/pct/01_single_sided_proton_ct_of_the_abdomen.py` was regenerated; `export_scripts.py --check` passes.
- **A dead link removed:** the tutorial no longer links the simulation's own Zenodo record (23814741), which isn't published yet.

## Results

SART noise and range error, a quarter of the protons against all of them:

| | Quarter (47 M) | All (188.6 M) |
|---|---|---|
| SART noise, liver | 0.051 | 0.028 |
| SART noise, kidneys | 0.043 | 0.026 |
| SART organ errors | −0.3 to −0.6% | −0.3 to −0.6% (unchanged) |
| SART range errors, 95% within | 2.78 mm | 2.08 mm |
| Run time (RTX 5090) | 43 s | 138 s |
| Peak RAM / GPU | 6.8 GB / 0.8 GB | 16.5 GB / 1.6 GB |

At 16.5 GB, the tutorial stays within the tutorials' 25 GB RAM limit.

## Checked

- The tutorial passed on 4.0.0 (this branch, installed), RTX 5090.
- `test_datasets.py` passes (48 tests), and the network link check passes for this dataset.
- `export_scripts.py --check` passes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b104217413a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.