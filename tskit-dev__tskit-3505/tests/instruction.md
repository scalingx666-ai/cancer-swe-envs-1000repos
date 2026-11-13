# Issue

**Title:** Allow an empty list of individuals in write_vcf

## Description

## Description

`ts.write_vcf(file, individuals=[])` (and `as_vcf`) raised `ValueError: No individuals specified`. With this change an empty list writes a sites-only VCF: every site with its REF and ALT alleles, and no `FORMAT` or sample columns (the `##FORMAT` header line is left out too). This works whether or not the tree sequence has individuals. Implicit cases still raise as before, for example individuals that have no nodes.

- `map_to_vcf_model(individuals=[])` returns an empty mapping instead of raising.
- `VcfWriter` writes only the fixed columns when the list is empty.
- The `write_vcf` docstring and `docs/export.md` now say that choosing a subset of individuals still writes every site, with REF/ALT taken from the whole tree sequence, and that `simplify` comes first if those sites should be dropped. They also describe the sites-only output.

Before:
```
>>> ts.as_vcf(individuals=[])
ValueError: No individuals specified
```
After:
```
#CHROM  POS  ID  REF  ALT  QUAL  FILTER  INFO
1       56   0   C    G    .     PASS    .
1       181  1   G    A    .     PASS    .
```
I also checked that pysam reads the output as a VCF with no samples and all sites.

## Tests

- `tests/test_vcf.py`: the old `test_empty_individuals`, which expected the error, now checks the sites-only output. New tests cover exact output with and without individuals in the tree sequence, and a name-count mismatch.
- `tests/test_highlevel.py`: `map_to_vcf_model(individuals=[])` with 0 and 2 individuals.

`pytest tests/test_vcf.py tests/test_highlevel.py -k empty_individuals`: 6 failed before the fix, 6 pass after it. `pytest tests/test_vcf.py tests/test_highlevel.py tests/test_cli.py` passes, and so do `ruff check` and `ruff format --check`.

# PR Checklist:

- [x] Tests that fully cover new/changed functionality.
- [x] Documentation including tutorial content if appropriate.
- [x] Changelogs, if there are API changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f29bfa1ca9c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.