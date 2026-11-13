# Issue

**Title:** Fix devtools check

## Description

A few devtools::check fixes:

  - Non-ASCII characters (—, …, ─) in R/main.R and R/reactable.R replaced with ASCII equivalents or \uXXXX escapes, clearing the checking code files for non-ASCII characters warning
  - All bare column name references that R CMD check flagged as "no visible binding for global variable" are resolved:
    - Bare dplyr column refs (GENOMIC_CHANGE, ASSERTION_AUTHORITY, CLASSIFICATION, CLINVAR_GOLD_STARS, CPSR_PATHOGENICITY_SCORE, SYMBOL, ALTERATION, VAR_ID, ENTREZGENE) replaced with .data$ pronoun
    - Temp columns created inside dplyr::mutate() (.clinvar_*, .override_*, .cpsr_overrides) made explicit by splitting the single mutate into two chained calls so each column is in .data before being referenced; subsequent rowwise() and case_when()
  blocks use .data$ throughout
    - tidyr::separate(MAXENTSCAN, ...) changed to tidyr::separate("MAXENTSCAN", ...) (quoted string)
    - dplyr::select(-.cpsr_overrides) changed to dplyr::select(-dplyr::all_of(".cpsr_overrides"))
    - setNames() and na.omit() qualified as stats::setNames() / stats::na.omit()

Also adds air.toml and Makefile

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fcbd05f890ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.