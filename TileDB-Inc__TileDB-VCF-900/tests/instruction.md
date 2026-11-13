# Issue

**Title:** Run nightly build with multiple python versions and reduce frequency

## Description

This PR adds Python 3.9 to the nightly builds. While we really only need it for testing with Linux, I couldn't decide whether it made more sense to test against the development versions of libtiledb/tiledb-py or the release versions. Knowing if it fails for one or both of these scenarios is part of the diagnostic power of the nightly build.

Thus I propose building all scenarios with both Python 3.9 and 3.14, but I'm happy to alter this to instead focus on only a single py39 build. To accommodate the increase in overall CI time, I reduced the nightly build frequency to [twice a month](https://crontab.guru/#0_3_1,15_*_*). Given the development frequency of TileDB/TileDB-Py/TileDB-VCF, I think this is sufficient to identify any potential compatibility problems.

xref: #899

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c80234338e64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.