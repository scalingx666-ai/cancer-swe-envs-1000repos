# Issue

**Title:** Use StringZilla byte lookup in Colorize

## Description

Use Albucore's shared uint8 lookup for each output plane in Colorize, then merge the planes into RGB. The batch path reuses plane storage across frames. Small single frames use the existing OpenCV path.

On M4 Max with unreleased AX and the R64 catalog adapter, a batch of 16 decoded frames took 2.01 → 1.73 ms through CPU collation. Including JPEG read and decode gave 33.46 → 33.13 ms. The 224×224 grayscale kernel took 53.6 → 31.4 µs. Outputs matched byte for byte.

The 45 focused Colorize and target contract tests and pre-commit passed. The AX performance skill and its copy of the canonical guide record the measured LUT routing tradeoffs.

## Summary by Sourcery

Optimize uint8 Colorize processing with shared LUT routing while preserving output compatibility across supported image layouts.

Bug Fixes:
- Preserve byte-for-byte Colorize output for batched, cropped, flipped, and read-only grayscale uint8 inputs.

Enhancements:
- Speed up uint8 Colorize processing by using shared Albucore/StringZilla lookup operations while retaining the existing OpenCV path for small images.
- Reuse channel-plane storage across batched frames and document LUT backend selection and benchmarking guidance.

Documentation:
- Document StringZilla-backed uint8 LUT guidance, channel-layout tradeoffs, and measured backend comparisons.

Tests:
- Add coverage for batched flipped grayscale views against Pillow Colorize output.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Performance**
  * Improved colorization performance for 8-bit images, including batches and non-contiguous image views.
* **Documentation**
  * Expanded guidance for choosing and benchmarking lookup-table approaches across image layouts, channel configurations, and output types.
* **Tests**
  * Added regression coverage for colorizing flipped, non-contiguous grayscale images.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d994b01eb20`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.