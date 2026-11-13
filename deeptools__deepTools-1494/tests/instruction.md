# Issue

**Title:** feat(alignmentSieve): opt-in --keepTags for shifted BAM output

## Description

- [x] Does the PR contain new feature?
 - [ ] Does the PR contain bugfix?
 - [x] Does the PR contain documentation changes?
 - [ ] Does the PR contain changes to the galaxy wrapper?
 - [x] Does the PR title follow [Conventional Commits](https://www.conventionalcommits.org/)?

This is the alignmentSieve half of the reverted #1485, split out and reworked after received input comments. It does not depend on the crate PR.

## What changes

New option `--keepTags TAG [TAG ...]`. With `--shift` or `--ATACshift` and BAM output it copies the named tags (for example `CB`) onto the shifted records. Without it nothing changes: SEQ, QUAL and all tags are dropped like on master. I did not touch the shift code itself.

Tags that describe the original alignment are refused with an error: `NM`, `MD`, `MC`, `SA`, `XA`, `CC`, `CP`, `CG`, `OA`, `OC`, `OP`, `TS`. The CIGAR is rewritten, so they would be wrong. `--keepTags` also errors without `--shift`/`--ATACshift` or together with `--BED`. The docs page has a new section on what shifted BAM output contains.

The use case is single-cell data, where the shifted reads still need their cell barcode.

## Potential Concerns

- **Performance.** The default path is untouched. On a 382 MB BAM (7.9M records, 8 threads) `--ATACshift --keepTags CB` took about 14 s against about 13 s for the default, so barely slower. Only `CB` is written, so the output stays small. These are a handful of runs on one machine, so treat the number as approximate.
- **Tags.** Only the "core" tags you are kept, and the alignment tags above are rejected instead of silently carried along.
- **Expanding shifts and shifts longer than the read.** My first version of the branch broke both (every read was dropped for `--shift -10 10` and `--shift 100 -100`). I reset the branch to master and redid it as an opt-in flag. I re-checked those shifts on `paired_chr2L.bam` and they behave as on master again.
- **Edge cases.** Documented in `alignmentSieve.rst`.

## How it was checked

- `cargo test --features python` and the alignmentSieve plus bamCoverage/bamCompare pytest files.
- New tests: tags dropped by default, `CB` kept with unchanged positions and values, alignment tags rejected, and the shift and BAM output requirement.
- Run on the large BAM above, checking that every record carries only `CB`.

## What requires further feedback

1. Is an opt-in flag the right shape, or would we rather change the default to keep a small set of tags?
2. I did not look at the mate fields (`mpos`, `tlen`) when only one read of a pair moves. That is master's behaviour and I left it alone, but we should know that code could be revised later on.
3. I haven't checked how the Galaxy wrapper would use `--keepTags`. Happy to add it here, or later.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13bf814ebd8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.