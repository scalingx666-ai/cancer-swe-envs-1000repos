# Issue

**Title:** 'candidate_fusion-genes_missing_mates.txt' deleted at 5849 but used at 7297

## Description

At line 5849 in `fusioncatcher.py` the   `candidate_fusion-genes_missing_mates.txt` file is deleted but is used elsewhere at line 7297, then deleted anyways at 11775:

At line 5849:
```   
 job.clean(outdir('candidate_fusion-genes_missing_mates.txt'),temp_path=temp_flag)
```
Line 7297:
```
job.add('--input_candidate_fusions_missing_mates',outdir('candidate_fusion-genes_missing_mates.txt'),kind='input',temp_path=temp_flag)
```
Line 11775:
```

    to_delete = [
        outdir('reads_mapped-exon-exon-fusion-genes_sorted-ref.map'),
```
...
```
        outdir('candidate_fusion-genes_missing_mates.txt'),
```
...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2589de4bd58d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.