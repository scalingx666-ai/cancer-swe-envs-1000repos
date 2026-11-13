# Issue

**Title:** perf(cds): use --threads in pyrodigal

## Description

Hi. Looks like prodigal -> pyrodigal (`f7aa6b9`) change didn't introduce --threads param so it is single-threaded. Looks like it does not change that much when running full platon but it's free speedup. I don't know this tool as much as bakta but maybe it is worth adding.

Tested with the `pyrodigal` command Platon uses, on megahit assemblies, 16 threads, cold cache:

| assembly | contigs | ORF prediction before | after | speedup |
|---|---|---|---|---|
| E. coli | 166 | 1.38 s | 1.04 s | 1.33x |
| ERR4333936 | 95,607 | 67.2 s | 47.8 s | 1.40x |
| ERR3607267 | 252,200 | 82.4 s | 62.2 s | 1.32x |

Thread scalability on ERR4333936:

| threads | time | speedup |
|---|---|---|
| 1 | 67.2 s | 1.00x |
| 2 | 56.5 s | 1.19x |
| 4 | 51.0 s | 1.32x |
| 8 | 48.0 s | 1.40x |
| 16 | 47.8 s | 1.40x |

Peak memory is unchanged. Output is identical except the `ID=` field in the FASTA/GFF headers, which encodes the work-queue order and which Platon discards when it parses the id (`functions.py`). Tests pass

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71d447a8fa5f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.