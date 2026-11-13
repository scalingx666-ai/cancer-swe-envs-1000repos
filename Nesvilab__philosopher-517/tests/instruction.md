# Issue

**Title:** Fix: Adjust I and L after razor assignment #

## Description

Propesed fix for issue #430 and issue #500 

To test the modifications I've made in philosopher I used the released (5.1.1) and the newly compiled philosopher and run FragPipe on a hela sample.

- First, I tested if the refactoring I made had any effects. I've compared the `psm`, `combined_ion`, `combined_peptide`, and `combined_protein` tables between the original and the refactored version and they were all identical.
- Next, I tested the version with the I/L fix. First, I looked at the `psm`, `combined_ion`, and `combined_peptide` tables, replaced all "I" with "L" in the sequences, sorted by the new sequence and compared the tables between the original and fixed version, they were identical.
- Finally, I checked if the I/L mixup was fixed in the `psm`, `combined_ion`, and `combined_peptide` tables. I used the "Start position" and "End position" columns together with the reported protein and extracted the expected peptide sequence from the FASTA file. Then I compared the expected with the reported sequences. For the current version (5.1.1) of Philosopher there were mismatches, whereas in the fixed version the I/L mixup was gone.

From what I could tell, it looks fine.

**Limitation**: For updating the sequence of modified peptide entries, I am assuming that modifications are always indicated by square brackets `[modification]` (and there are no additional square brackets within the modification, `[mod[i]fication]`). I couldn't find the definition of the pepXML schema, but at least in the FragPipe environment this seems to be the case.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d24d1a5c0214`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.