# Issue

**Title:** Added copy option besides soft or hard links.

## Description

There are two independent effects resolved with this merge request:

1. When using `-H hard` option (which is the default), I would expect all created links to be hard links - however, this is currently not the case, as some parts of the code create softlinks independent of the configured option (in particular the root `assembly_summary.txt`).
2. The genome update cannot be used on filesystems that do not support links, which expecially prevents direct download to many external hard drives without formatting the complete hard drive.

I suggest the following changes:
1. A new function `copy_or_link`, creating softlink, hardlink or copy of a file based on the passed configuration. The function is supposed to work only for files (`-T`), not for directories, in particular to prevent accidental deletion of directories.
2. Consistant use of this function at all places that created hardcoded softlinks before.
3. As a consequence, using the softlink path from `assembly_summary.txt` is no longer suitable to determine the active version if `-H hard` or `-H copy` has been used. Therefore, `current_label` is now determined from the last entry of the history file (`tail 1 | column 2`).

With the made changes and when using `-H copy`, I could download my database directly to an external harddrive with exFAT filesystem, which does not allow to create any type of links.  
  
If there is any good reason to keep the hardcoded softlinks instead, simply reject this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5eafcb3ecad2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.