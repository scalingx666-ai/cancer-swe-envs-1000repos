# Issue

**Title:** Support gzipped input and fix compiler errors in the unit tests

## Description

Hi,

I added some functionality to deal with gzipped input and solved some compiler errors in this pull request. This introduces an extra dependency to zlib and adds an external library that is downloaded automatically when compiling. Detailed changelog is included below.

Thanks for publishing this tool - I almost started implementing my own before stumbling upon yours :) 

## Changelog
Add support for using gzipped files as input ().
- Supported via the [bxzstr](https://github.com/tmaklin/bxzstr) library which replaces std::ifstreams in the code with bxz::ifstream. (commit )
- bxzstr is downloaded automatically when running cmake. The version of bxzstr is set at a fixed commit in config/CMakeLists-bxzstr.txt.in. (commit )
- zlib is now a required dependency when building but it should be available on all systems that process genome data anyway. (commits  and )
- Also supports reading files compressed with bzip2 and lzma if they are present on the system when compiling. Bzip2 and lzma are not required for building and support for them is detected and set automatically when running cmake.

Fixed compiler errors that happened on some systems with specific versions of GCC and Linux. (commits  and )

Added tests for gzipped input. (commit )

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a20855c2c230`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.