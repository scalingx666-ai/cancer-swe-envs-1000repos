# Issue

**Title:** Fix CI failures caused by fastq-dump/fasterq-dump segfault in sra-tools 3.4.x

## Description

`sra-tools` 3.4.1 introduced a segmentation fault regression in both `fastq-dump` and `fasterq-dump` when downloading SRA accessions, causing the sra2fastq tests to hard-fail and — due to `--maxfail=2` in pytest addopts — abort the entire CI run.

## Changes

- **Pin `sra-tools<3.4`** in both `main.yml` and `sra2fastq.yml` to avoid the broken 3.4.x versions
- **Graceful skip on tool failure** in all four `test_sra2fastq*.py` tests — `subprocess.CalledProcessError` and the bare `Exception` raised by `isPairedSRA` are now caught and converted to `pytest.skip()` with the exception message preserved for diagnostics:

```python
try:
    converter(method=method)
except (subprocess.CalledProcessError, Exception) as e:
    pytest.skip("sra-tools crashed or failed (possible segfault or network issue): {}".format(e))
```

The skip approach provides defense-in-depth: if a future sra-tools release regresses again (or NCBI has transient issues), the tests degrade to skipped rather than breaking the full suite.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46e6040b876b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.