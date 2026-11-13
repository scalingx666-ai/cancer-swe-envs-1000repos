# Issue

**Title:** Blocklist

## Description

This PR implements a per-query blocklist/unblocklist for operations which compare a set of query sequences to a database, i.e., usearch_global, usearch_local, and sintax.

The lists are specified using `-blocklist` and `-unblocklist` followed by a file name. Files should contain on each line the sequence name of a query sequence, followed by a tab and then one or more comma-delimited taxon or sequence names from the target database. If the same query sequence appears on multiple lines, those lines are combined. Taxon names should include the letter indicating their taxonomic rank, e.g. "f:Saccharomycetaceae".

The results of a search/classification operation where some sequences/taxa are in the blocklist are identical to the situation where those sequences were entirely removed from the database; however different blocklists can be specified for each query and they are run in a single program invocation without reloading the database or rebuilding the index.

The `-unblocklist` option can only be given if  `-blocklist` is given.  Its function is to add back in a subset of the blocklist taxa/sequences; for instance to create a situation where an entire genus is removed by the blocklist, but one particular species or sequence from that genus is retained.

Benchmarking with a difficult blocklist (i.e., 500k database sequences, 1000 queries, many queries have blocklisted taxa which cover >50% of the database including all close matches) showed ~2x slowdown for usearch_global and ~5x slowdown for sintax, both relative to `-self`.  The PR gives a minor performance hit relative to master (~3%) for these functions when no blocklist option is given.

The purpose of these options is taxonomically structured testing or calibration, e.g. "How well can we identify sequences at the family level if we remove all references from the same genus". In particular the per-query blocklist + unblocklist combination allows generation of model training data for [Protax](https://doi.org/10.1093/bioinformatics/btw346) models using usearch_global and sintax as predictors, such as [ProtaxFungi](https://doi.org/10.1111/nph.15301).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c62ff2b3050`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.