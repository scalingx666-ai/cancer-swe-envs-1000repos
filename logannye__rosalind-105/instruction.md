# Issue

**Title:** Account for complete CRAM decoder state and validate index coverage

## Description

CRAM decoding retains complete slices and off-target records, so the old per-record allowance could underestimate its memory. The corrected engine validates whole-file structural/container/index bounds and every record, then derives indexed and worker reservations from verified maxima. It rejects stale CRAI coverage instead of returning false zeros and preserves scientific filters and output bytes.

The fresh packaged rerun also exposed a native rust-htslib indexed-reader lifetime crash. Commit `9b8e12f3b6e802d2103c5ebeb5ff89a08c8d85ce` adds a private owner that destroys the iterator and CRAM index before closing their borrowed file, preserving the existing Send contract and pinned ABI. The new eight-worker lifetime regression reproduces SIGSEGV on the previous `9862692` source and passes on the corrected source.

Corrected validation: 108/108 HG002 representative runs pass with zero baseline output-hash differences and zero prediction underestimates; 14/14 real Linux cgroup scenarios pass; 31 Linux focused tests pass; installed Python3.9 and3.11 each pass23 tests; packaged analyzer onboarding passes including all19 evidence conformance checks. Native CRAM validation can still allocate before a cooperative checkpoint; no universal allocation sandbox is claimed.

[Retained verified report and raw artifacts](https://github.com/logannye/rosalind/blob/bc6e9e6/docs/findings/cram-decoder-validation-2026-09-06/verified-9b8e12f-2026-09-18/README.md) are included in the dependent documentation PR #143. The prior failed attempt remains byte-identical and separate. Local Linux validation uses an existing Colima VM on the same physical workstation, not an independent machine. These results do not establish publication or adoption.

PR #104 is merged; this PR now targets main. Source is frozen at the corrected commit above and its complete supported CI matrix must pass before merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87fa81ecf050`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.