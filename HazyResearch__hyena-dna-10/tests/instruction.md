# Issue

**Title:** Speed-up Genomic Benchmarks dataloader

## Description

I've modified the dataset class such that sequences are simply stored in a list and indexed from memory rather than being read from file. With this change I observed a speedup in epoch time of up to ~ 5x

| Dataset                             | Epoch time (old) | Epoch time (new) |
|-------------------------------------|------------------|------------------|
|   dummy_mouse_enhancers_ensembl     |   3s             |   2s             |
|   human_enhancers_cohn              |   42s            |   14s            |
|   human_nontata_promoters           |   49s            |   10s            |
|   demo_coding_vs_intergenomic_seqs  |   2m 6s          |   25s            |
|   demo_human_or_worm                |   2m 19s         |   25s            |
|   human_enhancers_ensembl           |   3m 56s         |   1m 20s         |
|   human_ocr_ensembl                 |   4m 48s         |   1m 32s         |
|   human_ensembl_regulatory          |   8m 21s         |   2m 37s         |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7016972bf8e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.