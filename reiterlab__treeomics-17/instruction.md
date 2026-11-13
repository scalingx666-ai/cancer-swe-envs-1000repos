# Issue

**Title:** More unique driver gene identification method

## Description

Hi Hannes, 

As we discussed I have made changes to treeomics to identify drivers by location (e.g. 12:25380275) rather than just gene name. For this, the user has to input a csv file containing the driver gene information output by CRAVAT. Specifically this csv file has to have headers: "Gene_Symbol" (e.g. KRAS) and "Mutation_Location" (12:25380275).

I also made the code read in the nucleic acid sequence change (A>T) as well, just in case we want to use that as an identifier as well down the road. The user should have this column named as "Change"

Hope this will help!

Best,
Haochen

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd11cb709667`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.