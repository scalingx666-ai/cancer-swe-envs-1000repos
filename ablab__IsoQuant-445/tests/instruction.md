# Issue

**Title:** fix redundant junction profile computation

## Description

## Summary

`GeneInfo.set_junction_profiles` wraps its per-transcript loop in `for gene_db in self.gene_db_list:`. The loop body never uses `gene_db`, and it iterates over `self.all_isoforms_exons`, which already holds the transcripts of every gene in the cluster. 

This PR removes the redundant outer loop. Each transcript's profiles are now computed once.

## Behaviour

No functional change. Each repeated pass produced identical values for the same keys. 

## Performance

Tested on a small BAM with 12k records from 2 chromosomes

### wall time   
```
Isoquant 4.1.0    23m 33s
this patch        2m 31s
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cea5337ea4e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.