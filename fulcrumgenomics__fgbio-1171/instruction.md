# Issue

**Title:** fix(umi): AnnotateBamWithUmis should not fail on UMIs without BAM records

## Description

.

With `--sorted`, a UMI in the FASTQ that has no corresponding BAM records was counted as a *missing UMI* and caused a non-zero exit with `Execution failed!`, even though the output BAM was complete and correctly annotated. This is the ordinary case when an upstream tool discards read pairs, and it contradicts the tool's own documentation: *"If no BAM reads exist for the UMI, no logging or error will be reported."*

The two conditions were sharing one counter, so the log message was also backwards — it reported "missing UMIs" when what was actually missing was *reads*. They are now tracked separately:

- **A UMI with no BAM records** is skipped, counted, and reported (`Skipped N UMIs with no corresponding records.`), and is not an error. This also correctly scopes `--fail-fast`, which is documented for BAM records without a matching UMI.
- **A BAM record with no UMI** remains counted, logged, and a non-zero exit.

This also changes `--fail-fast`: it no longer triggers on a UMI without BAM records, and in sorted mode it now names the read it failed on. Previously the sorted path could not report that condition at all — it died with `No more FASTQ records but more SAM records` instead. `--fail-fast` had no test coverage anywhere in the repo; it is now tested in both modes.

## History

This is a reintroduced regression, not a new bug. #735 fixed it in Oct 2021 (`records.nonEmpty`) and added the documentation sentence above; #657 rewrote the `--sorted` block for multi-FASTQ support two months later and restored `records.isEmpty` → `logMissingUmi`, reverting the fix while keeping its documentation. #735's fix therefore never appeared in a release: 1.4.0 predates it and 1.5.0 postdates the revert. The `while (samIter.hasNext)` guard added by #1055 covers extra FASTQ records only at the *end* of the file, so records in the middle — the reported case — still failed.

## Two related fixes

- **Output truncation.** A BAM record absent from the middle of the FASTQ consumed the remainder of the FASTQ looking for a match, then failed with `No more FASTQ records but more SAM records` *before* `out.close()`, leaving a zero-record output BAM. Remaining BAM records are now written out un-annotated before failing, matching the un-sorted path, which has always written records that had no UMI. The trailing `samIter.foreach` that was meant to do this was unreachable and never wrote records; it is now reachable and does.
- **Exit code and diagnostics.** `fail(exit=missingUmis.toInt)` exited **0** whenever the count was a multiple of 256 — logging `Execution failed!` while reporting success — and overflowed past 2^31. Failures now go through `fail(message)`, which takes exit 1 from `FailureException`'s default and prints the reason inside the fatal block, instead of leaving `Execution failed!` with no explanation.

Note that with equality-only name matching (`--sorted` promises identical order, not lexicographic sort) a BAM record missing from the middle of the FASTQ still costs the UMIs of every record after it. That remains a loud, counted failure with a complete output BAM, rather than a silent truncation.

## Tests

The tests for extra FASTQ records deserve their own note, since they are why the revert went unnoticed for four years.

- From #735 until #1047 they never called `annotator.execute()` — they constructed the tool, then iterated the empty temp file `makeTempFile` had created, which yields zero records without throwing. They passed unconditionally, which is how #657 reverted the fix with CI green. #1047 spotted this and commented the `--sorted` one out with `// TODO: write a test that actually tests this behavior.`; #1055 re-enabled it.
- Once re-enabled, the extra FASTQ record was appended to the **end** of the file, exactly the case the `hasNext` guard short-circuits before reaching it. Nothing covered a record mid-FASTQ.
- The multi-FASTQ "extra lines" test called `Io.writeLines` twice, and the second call overwrote the first — so the FASTQ held only the extra record, and the test passed for a reason unrelated to its name.

Added or repaired:

- extra UMI **mid-FASTQ**, single- and multi-FASTQ (both previously failed; the multi-FASTQ one is the repaired overwrite test, now asserting success)
- all records are written whether or not they were annotated, guarding the truncation bug (previously produced 0 of 10 records)
- record counts asserted alongside tag values, so a silently empty output BAM can no longer pass

Also folded into this change: the new missing-UMI test was byte-for-byte the existing `"fail if one or more reads doesn't have a UMI when the fastq is sorted"` test plus one assertion, so the two are now one test; FASTQ fixtures are built from `FastqRecord` via `FastqWriter` rather than raw lines, so record boundaries are no longer magic line counts (`grouped(4)`, `dropRight(8)`); reads-back use the existing `UnitSpec.readBamRecs`; and `numSamRecords` is derived from the fixture rather than hardcoded.

One failure assertion was deliberately dropped: the multi-FASTQ "extra lines" test called `Io.writeLines` twice and the second call overwrote the first, so its FASTQ held only the non-matching extra record — it asserted failure on "FASTQ far shorter than BAM", not on extra lines as its name claimed. That scenario stays covered by the multiple-truncated-FASTQs test; the repaired test now asserts the success its name always described.

Each new test was confirmed to fail against the unfixed code, both before and after that refactor. Full suite passes: 1614 tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5964919673c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.