# Issue

**Title:** Preserve coordinates through partial reverse sequence slices

## Description

Partial slices with step `-1` calculate coordinates from the stop index alone, without accounting for the selected start or original orientation. The bases can be correct while the labeled interval is wrong, and another slice can then raise `ValueError`:

```python
from pyfaidx import Fasta

with Fasta('tests/data/chr17.hg19.part.fa') as fasta:
    part = fasta['chr17'][100:110].reverse[8:2:-1]
    print(part.fancy_name)
    print(part[:].seq)
```

Before: `chr17:99-112`, followed by the coordinate-length error. After: `chr17:102-107` and `CTGGGC`.

Calculate both endpoints from the normalized selected indices and the original direction, retaining the existing adjustment for inclusive versus half-open coordinates. Forward slicing and the omission of coordinates for non-unit strides remain unchanged. This extends the orientation handling added in #242 to partial reverse slices.

The added regressions cover both coordinate conventions, both directions, complements, partial/default bounds and continued slicing. Public chromosome/transcript workloads agree with independent per-base coordinate lists; complete controls and CLI outputs stay unchanged. The configured suite and doctests pass on Python 3.9, 3.12 and 3.13. An installed wheel and a local composition with the separate record-slicing fix (#247) reproduce the results.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7231d50560c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.