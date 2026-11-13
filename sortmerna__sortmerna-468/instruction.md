# Issue

**Title:** Read the last line of a reads file that has no final newline

## Description

.

`build_chunk_offsets` and `build_flat_chunk_offsets` split a reads file into slot byte ranges at the offset just past each `'\n'`. A last line with no `'\n'` was never counted as a line, so no slot's range reached it and it was never read. As a result, a FASTA record lost its last sequence line (a single-line record became empty), and a FASTQ record lost its quality line. This change counts such a line as ending at EOF, in both functions.

### Tests

- **New tests.** `test_run_fasta_without_final_newline` and `test_run_fastq_without_final_newline` each run the same reads through `smr_run` twice, with and without a final newline: a multi-line FASTA record, and a two-record FASTQ. Both runs must give the same alignments and the same SAM records. Without the fix, both tests fail: the FASTA one ends at reference 1399 instead of 1446, and the FASTQ one loses the second record's QUAL.
- **Regenerated goldens.** `tests/golden/tiny` and `tests/golden/small/other.fa` held the dropped line (the comment removed here from `test_smoke.c` described it). I regenerated them with the CLI and the arguments in the `@PG` line, and only the affected records change:
  - AB271211 now aligns to reference 1446 (`…1260M`, AS 2430), the same as its reverse complement in `test_run_reverse_strand`.
  - `random2` has its sequence in `other.fa`.

  `test_run_tiny_per_read_output` and `test_run_tiny_strand_score_edit` are updated to match.
- **Test results:** `ctest` 2/2 on macOS arm64; `smr_api_smoke` ran 103 tests with 0 failures.
- **Checked by hand with the CLI:**
  - gzipped FASTA and FASTQ without a final newline now read every line;
  - an empty reads file is still rejected by option validation, as before.

The `41S16I` at the start of the tiny CIGAR is a separate problem and is unchanged here: parasail's traceback reports a leading insertion when it leaves the reference window first.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0944692ea69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.