# Issue

**Title:** JDBC: bump sqlite-jdbc pin to 3.54.1.0

## Description

Release step 0 advance for v0.10.0: the pinned sqlite-jdbc version moves from 3.53.4.0 to 3.54.1.0, the current Maven Central release, whose bundled engine matches the SQLite 3.54.1 this release already ships. Verified at the source: the 3.54.1.0 jar's checksum matches Central's published value, and its base classes remain Java 8 bytecode (the only newer classes are GraalVM native-image entries in the multi-release versions directory), so the Java floor is unchanged. CI's JDBC tests exercise the binding against the new pin.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7e1b11f1412`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.