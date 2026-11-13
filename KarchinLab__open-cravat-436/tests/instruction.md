# Issue

**Title:** Fix 500 when deleting jobs that have no celery task

## Description

Deleting a job from the Jobs table fails with HTTP 500 when the job has no celery_id in its status.json. This affects jobs imported from another install and jobs run before the celery-based GUI.

Cause: Job.task returns None when there is no celery_id, and delete_job in cravat/gui/submit/handlers.py read job.task.cravat_status unconditionally, raising AttributeError before the job folder was removed.

Fix: guard the status-polling loop with job.task is not None, so those jobs fall through to rmtree.

Observed on 3.2.1: 19 of 20 jobs in one jobs directory had no celery_id, and all failed to delete. The fix was applied to the installed copy and confirmed working.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3aa9a3e64b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.