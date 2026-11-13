# Issue

**Title:** Restore SIGPIPE handler in createTHetAExomeInput.py

## Description

This fix addresses a problem regarding broken pipe messages that has been discussed on the Google Groups help forum. See,

https://groups.google.com/forum/#!topic/theta-users/GwfdoQBTkYo

The function get_read_length() creates a POSIX pipe via the subprocess
module can cause exceptions to be raise as Python has redefined the
signal handler for SIGPIPE to ignore this signal.  This fix restores
the signal handler for the subprocess calls.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02be79ea1f8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.