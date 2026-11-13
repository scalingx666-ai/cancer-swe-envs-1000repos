# Issue

**Title:** Iterator failures should raise an exception, rather than simply write to stderr

## Description

`sam_itr_next` returning an error is generally fatal, due to a corrupted BAM or filesystem instability. The current approach of simply logging to stderr is suboptimal, since it means that any iterator failures cannot be caught and handled by whatever is invoking `Bam.query()`.

(See , which relies on these exceptions being thrown to cause a nonzero exit upon iterator failure.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c7a004572ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.