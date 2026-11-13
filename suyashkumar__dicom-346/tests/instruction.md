# Issue

**Title:** Allow unknown specific character set to default to UTF-8 encoding when parsing

## Description

This change implements an option to allow an unknown specific character set when parsing a DICOM and fallback to using UTF-8.

For context, in my application of this parser, we are seeing erroneous specific character sets such as
```
ISO IR 192
ISO_2022_IR_6
NONE
```
Current behaviour is that parsing fails immediately upon encountering an unknown character set, and the error also indicates that it will fallback to utf-8 (which is misleading since it just errors out instead of actually falling back). It seems there was a `TODO` in place for this, so this change implements the option to allow this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37f0671f9dd1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.