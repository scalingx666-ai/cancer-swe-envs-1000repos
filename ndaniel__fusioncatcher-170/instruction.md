# Issue

**Title:** Changed how BBmap version is checked

## Description

Changed to using BBversion.sh for checking the version of BBmap.sh. 

The reason was that I was having problems running fusioncatcher on a cluster using SGEs qsub. I believe the problem lies in how STDOUT and STDERR works when submitting through qsub, making it problematic in redirecting both STDOUT and STDERR to the bbmap_version.txt file.

Instead using bbversion.sh alleviates this issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5813f67bc075`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.