# Issue

**Title:** Disable IMDS in the nightly workflow

## Description

The AWS credential chain includes the EC2 Instance Metadata Service (IMDS) by default. Since the runners are not on EC2 these requests fail. On Linux the requests fail fast but on the macOS runner they block until the response timeout. This compounded with the unreleased TileDB 2.31 (i.e. `main`) changes to the VFS S3 retry strategy causing the run-time of the TileDB-VCF nightly workflow to balloon on the macOS runner. Specifically, the `tests/test_config.py::test_large_export_correctness` test was hitting this codepath when accessing the S3 bucket holding the test data and blocking all other tests while waiting on IMDS.

This PR also revealed two upstream bugs worth following up on in the TileDB repo:
- **TileDB probes the EC2 instance metadata service (169.254.169.254) from inside the held `S3::init_client()` mutex**, so on any non-EC2 macOS host — where that probe blocks until timeout rather than failing fast as on Linux — a single  `Group`/array open convoys the entire thread pool behind it, costing 192s on 2.30.1 and over 300s on 2.31.0 versus ~3s on Linux.
- **TileDB PR #5747's switch to the AWS SDK's `standard` retry strategy leaks retry quota** — 5 tokens spent per retry but only one retry's worth refunded per successful request, so a workload needing 2 retries each hard-fails at exactly request 100 — and it silently doubled the credential-provider retry budget from 5 to 10 by dropping the `vfs.s3.connect_max_tries` default, a path that `vfs.s3.retry_strategy` cannot reach.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84d62dd1c542`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.