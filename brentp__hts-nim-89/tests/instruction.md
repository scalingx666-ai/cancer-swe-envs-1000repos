# Issue

**Title:** Support Nim 2.2.4 (test fisher fails)

## Description

Fix for #88 

in Nim 2.2.4 temporaries are no longer allowed; result.left.cdouble creates a temporary C double value

Tested using Nim 1.6.6, 2.0.4 and 2.2.4 under:
* MacOS (Apple Silicon) using htslib 1.22.1 (from conda)
* Ubuntu 24.04.1 LTS using htslib 1.19 (from apt)

I noticed that i had to run 
```
nim c --mm:refc  -d:useSysAssert -d:useGcAssert --lineDir:on --debuginfo -r tests/all
```
twice in Ubuntu and the frist time failed complaining about missing files from Readme (`[FAILED] Compile Readme sample`), the second passed. 

I put it here in case this is not ok.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29f0998b0390`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.