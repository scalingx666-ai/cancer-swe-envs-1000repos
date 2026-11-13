# Issue

**Title:** Switch build_dbs.py to boto3, add Pfam-A.clans.tsv auto-download, replace MySQLdb with mysql-connector-python

## Description

- [x] Add `boto3` and `mysql-connector-python` to `requirements-dev.txt`
- [x] Update `bin/build_dbs.py` to use boto3 for S3 operations directly (no wrapper functions), credentials from environment
- [x] Update `bin/build_dbs.py` to download `Pfam-A.clans.tsv` from S3 if it doesn't exist locally
- [x] Update `bin/build_dbs.py` to use `logging` instead of `print` statements
- [x] Update `agfusion/database.py` to use `mysql-connector-python` instead of `MySQLdb`, with error handling

<!-- START COPILOT ORIGINAL PROMPT -->

<details>

<summary>Original prompt</summary>

> Update the #file:build_dbs.py file with the following requirements:
> - Have it use the boto3 aws library when download/uploading any files from s3. it can assume credentials come from environemnt variables. boto3 should only be a dev dependency in #file:requirements-dev.txt
> - Have it download download the 'Pfam-A.clans.tsv' file from the s3 bucket if it does not exist locally
> - Update #file:database.py to use mysql-connector-python instead. It should have that dependency installed in #file:requirements-dev.txt
> Create a pull request.
>
> The user has attached the following file paths as relevant context:
>  - requirements-dev.txt
>  - agfusion/database.py
>  - bin/build_dbs.py
>  - .github/instructions/python.instructions.md
>  - .github/copilot-instructions.md

</details>

<!-- START COPILOT CODING AGENT SUFFIX -->

Created from [VS Code](https://code.visualstudio.com/docs/copilot/copilot-coding-agent).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1ac6152f5f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.