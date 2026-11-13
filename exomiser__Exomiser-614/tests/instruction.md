# Issue

**Title:** Ph/re scale boqa raw log score

## Description

I implemented the following method to re-scale the BOQA scores so that they can be combined with the variant score in Exomiser.

<img width="1226" height="123" alt="image" src="https://github.com/user-attachments/assets/dac09064-dfbe-4136-8000-057c9d4b8ddc" />

The boqaRawLogScores are calculated directly in BOQA from the four counts to avoid numerical instabilities.

This score has the following properties:

1. Exomiser compatible: The maximum score is always 1.0, the lowest is 0.
2. BOQA's ranking remains unchanged.
3. The original BOQA scores are somehow reflected in the transformed BoqaExomiserScore (which is not the case with rank scaled score).

Here is the distribution of scores across ranks for 3000 phenopackets from phenopacket-score for which BOQA ranks the diagnosed disease first.

<img width="605" height="472" alt="image" src="https://github.com/user-attachments/assets/27880776-8adf-4e42-ad46-308989ea6e18" />

To implement this, I added a function in BOQA `BoqaPatientAnalyzer` that provides the BoqaPrioritizer in Exomiser with unnormalized BOQA log scores. See here:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `984691f3541f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.