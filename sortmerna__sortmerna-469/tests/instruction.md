# Issue

**Title:** Soft-clip leading insertions in parasail CIGARs

## Description

Builds on #468, which changes the same golden lines. Its commit is included here until it merges, so please review only the last commit (2d74934).

When parasail's traceback leaves the reference window before the query, `parasail_result_get_cigar` reports the remaining query bases as a leading `I` run. A local alignment never starts with an insertion, so the score is that of the alignment without it, while the CIGAR, read start, NM, identity and coverage describe a different one. This strips leading `I` ops and advances `read_begin1`, as is already done for leading `D` ops.

`test_data/test_read.fasta` against `test_data/test_ref.fasta`:

| | CIGAR | NM | identity | coverage | AS |
|---|---|---|---|---|---|
| before | `41S16I57M2I12M…1260M` | 110 | 92.5 | 97.2 | 2430 |
| after | `57S57M2I12M…1260M` | 94 | 93.5 | 96.2 | 2430 |

SortMeRNA 4.4.0 also reported `57S57M2I12M…` for this read.

### Tests

- `tests/golden/tiny/aligned.{blast,sam}` regenerated with the CLI and the `@PG` arguments; only AB271211's record changes. `tests/golden/small` is unchanged.
- `test_run_tiny_per_read_output`, `test_run_tiny_strand_score_edit` and `test_run_reverse_strand` updated to match. The CLI gives the reverse complement the same values (FLAG 16, AS 2430, NM 94).
- `ctest` 2/2 on macOS arm64. With the fix and the old expectations, five tests fail: those three, `test_golden_tiny_blast` and `test_golden_tiny_sam`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `847cee400b39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.