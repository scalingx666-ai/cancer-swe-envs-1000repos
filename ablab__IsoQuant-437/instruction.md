# Issue

**Title:** Keep read tags when aligning reads and warn when the polyA tag is missing

## Description

/ #429. `--polya_trimmed tag:pt` had no effect when IsoQuant aligned the reads itself: minimap2 ran without `-y` and `samtools fastq` without `-T`, so Dorado's `pt:i` never reached the BAM, and IsoQuant fell back to sequence-based detection without saying so.

## Changes
- **Read tags are kept by IsoQuant's minimap2 step, regardless of `--polya_trimmed`.** This lets a BAM from an earlier run be reused with tag-based options without realigning, which takes longer than the rest of the pipeline.
  - Unaligned BAM (`--unmapped_bam`): `samtools fastq -T <tags>` | `minimap2 -y`. The tags are collected from the first 1000 reads.
  - FASTA/FASTQ (`--fastq`): when the header comments of the first 1000 reads are all tab-separated SAM tags (as in Dorado `--emit-fastq` output), `samtools import -T` | `samtools fastq/fasta -T` | `minimap2 -y`. Other files are passed to minimap2 directly, as before. FASTA stays FASTA, so no fake qualities are added.
  - Tags minimap2 writes itself are not copied: Dorado's `ts:i` would clash with minimap2's `ts:A`. `RG`/`PG` are not copied either, because the header lines they refer to are not carried over.
  - The three separate process-pipe blocks are now one helper, `run_piped_commands`, with the same error messages and exit codes.
- **Warning:** with `--polya_trimmed tag:X`, IsoQuant warns when none of the first 1000 primary alignments of a BAM carry X. The warning explains how to fix it: `--clean_start` for alignments cached from earlier runs, or `samtools fastq -T | minimap2 -y` when aligning yourself.
- **Docs:** `docs/cmd.md` (the tag must be present in aligned reads), a new "Read tags" section in `docs/input.md`, `changelog.md`.

## Notes
- Modified-base tags (`MM`/`ML`) are kept when present, which can make the BAM noticeably larger.
- Requires a samtools with `import -T`; tested with 1.13.

## Testing
- New unit tests in `isoquant_tests/test_read_tags.py`. They have not been run locally yet.
- Manual check: aligned small tagged FASTQ, gzipped FASTQ, FASTA and unaligned BAM inputs to `chr9.4M`. `pt` reached all alignments in each case, and `ts:i`/`RG` were dropped. The warning fires on `chr9.4M.ont.sim.polya.bam`, which has no `pt` tag, and stays silent on the tagged output.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e508a04eea0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.