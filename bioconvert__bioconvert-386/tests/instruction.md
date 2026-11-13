# Issue

**Title:** Fix genbank2gff3 wrong Parent when `gene` follows its RNA/CDS feature

## Description

`genbank2gff3` assumed the `gene` feature comes before its `tRNA`/`mRNA`/`rRNA`/`CDS`. When a gene was listed after its RNA (as in antiSMASH output), the RNA got the previous gene as its `Parent`. If the RNA came first in the file, the conversion failed.

Example input (`tRNA` before `gene`):

```
     tRNA            243644..243717
                     /locus_tag="OIE51_01175"
     gene            243644..243717
                     /locus_tag="OIE51_01175"
```

Before: `Parent=OIE51_01170`. After: `Parent=OIE51_01175`.

Changes in `bioconvert/utils/biocode/convert_genbank_to_gff3.py`:

- **Gene index:** before processing each record, build the genes keyed by `/locus_tag`. The `gene` branch reuses the pre-built object instead of creating a new one.
- **Parent resolution:** a non-`gene` feature with a `/locus_tag` is attached to the gene with the same locus tag, wherever it is in the file. If no gene shares the locus tag, it falls back to the most recent gene, as before. `current_RNA` is reset only when the gene actually changes, so multi-exon `CDS` handling is unaffected.
- **Output order:** genes are now written at the end of the run, in order of first appearance, rather than as each next gene is reached. Gene order is unchanged. Each gene's children still follow it.

No regression test is added in this PR.

<!-- START COPILOT CODING AGENT SUFFIX -->

-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `92f4655cc75a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.