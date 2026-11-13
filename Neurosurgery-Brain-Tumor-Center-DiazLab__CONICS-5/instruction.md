# Issue

**Title:** remove http prefix

## Description

In my hands (R 3.4.1, CONICSmat_0.0.0.1), these http prefixes cause the following error:

```
Request to BioMart web service failed.
The BioMart web service you're accessing may be down.
Check the following URL and see if this website is available:
http://http://dec2016.archive.ensembl.org:80/biomart/martservice?type=registry&requestid=biomaRt
Error in if (!grepl(x = registry, pattern = "^\n*<MartRegistry>")) { :
  argument is of length zero
```

Dropping the http fixes that issue

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eec3c6af6c98`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.