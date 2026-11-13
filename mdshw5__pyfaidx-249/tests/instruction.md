# Issue

**Title:** Preserve coordinates and bounds when indexing individual bases

## Description

Integer indexing of a `Sequence` has its own coordinate calculation, which increments labels even for a reversed sequence and always uses inclusive endpoints. It also treats a zero or absent start as a positional complement argument. An overly negative index is normalized twice and can return a base instead of raising:

```python
from pyfaidx import Sequence

sequence = Sequence('chr1', 'ACGTA', start=1, end=5).reverse.complement
print(sequence[1].fancy_name)
# Before: chr1:6-6 (complement); after: chr1:4-4 (complement)
print(sequence[-6])
# Before: T; after: IndexError
```

Check the normalized bounds, then use the existing one-base slice path. This preserves forward/reverse coordinates under both attribute conventions, complement flags, and the absence of coordinates. Update the zero-based indexing doctest and add regressions for labels, complements, empty sequences and out-of-range indices.

The full pytest suite and doctests pass on Python 3.9, 3.12 and 3.13. Extraction from real chromosome/transcript FASTA data agrees with independent raw per-base labels, Biopython complements and native HTSlib fetches across plain/BGZF files and read-ahead modes. All previously working extraction records and parent sequences remain exact; an installed wheel gives identical results. Other platforms and the separate acidbio suite were not run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `98ad0718ddc8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.