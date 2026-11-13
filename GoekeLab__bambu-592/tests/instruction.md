# Issue

**Title:** fix bugs and update contact for devel branch

## Description

## Related Issue
[Bioconductor build error](https://bioconductor.org/checkResults/devel/bioc-LATEST/bambu/)


## Type of Change
- [x ] **Bug fix** (non-breaking change which fixes an issue)

## Description
Fix 2 bugs: 
- ggbio plot annotation issue causing bioconductor build error
- BSgenome is required to do look up, and that requires internet access 

Update contact email addresses

## Implementation Details
For bugs:
-  fix by disable ggbio related functions in vignettes and unit test function
- only activate look up for genome through BSgenome packge when fasta file is not a local existing file to avoid the need for internet access for BSgenome 


## Impact of Changes
- Results are identical to the previous version.
- Bug fix only (no changes to output).


## Checklist
- [x] My code follows the style guidelines of this project.
- [x] I have performed a self-review of my own code.
- [x] I have verified that GitHub automated tests passed. (Describe any failing tests in the next section)
- [x] I have commented my code, particularly in hard-to-understand areas.
- [ ] I have made corresponding changes to the documentation (vignettes, man pages).
- [ ] I have tested the code on a full dataset, and any differences have been described in the pull request.

## Post-merge follow-up
- plotBambu function not working properly for plot annotations, consider to submit proper fix later

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `066b92ff222d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.