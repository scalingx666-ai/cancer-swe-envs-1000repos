# Issue

**Title:** CTM-649 Clean up CWL complexity in standard streams

## Description

### Description

I am working on Cromwell-defined limits to control how many logs a task can stream to Cloud Logging. This is a behavior-unchanged cleanup ahead of that work.

In 2022 we landed PR  to clean up most CWL. It  for `stdinRedirection` / `stdoutOverride` / `stderrOverride` but left the plumbing in place.

### Release Notes Confirmation

#### `CHANGELOG.md`
 - [ ] I updated `CHANGELOG.md` in this PR
 - [x] I assert that this change shouldn't be included in `CHANGELOG.md` because it doesn't impact community users

#### Terra Release Notes
 - [ ] I added a suggested release notes entry in this Jira ticket
 - [x] I assert that this change doesn't need Jira release notes because it doesn't impact Terra users

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66e81f268e1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.