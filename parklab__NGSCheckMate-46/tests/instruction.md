# Issue

**Title:** Incorporate bug fixes and update version number

## Description

This pull request incorporates the bug fixes included in #31, #37, as well as some further changes:
I have been using this version "in production" for the last 2 years, running over 3000 samples through NGSCheckMate in batches. The tool is extremely useful, and I am ready to include it into several Nextflow workflows in the nf-core community, but can not without the fix that #31 provides to prevent divide by zero crashes in particular.

@SooLee , please can you take a look at this PR, and release a new version of the tool.

* BAM mode no longer crashes if samples with few reads (i.e. failed samples) is provided, causing a divide by zero error (incorporating #31)
* split the directory only once if the dir contains "=" in the name (incorporating #37)
* The `output_tag` prefix is added to the `output_corr_matrix.txt` file 
* Making the size of the dendrogram pdf scale better as more (100+) samples are added
* Ensured a dendrogram is generated if only two samples are compared 
* Changed the dendrogram background colour to white from grey
* Updated the version information from v1.0 to v1.0.1

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ea2c043896a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.