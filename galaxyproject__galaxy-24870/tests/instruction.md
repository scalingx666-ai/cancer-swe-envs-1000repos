# Issue

**Title:** [26.1] Merge release_26.0 into release_26.1

## Description

Merges `release_26.0` into `release_26.1`.

## PRs brought in

- #24835 Send one summary email for jobs mapped over a collection
- #24842 (merge of `release_25.1` into `release_26.0`; already on 26.1 through #24843)

## Conflicts

None. I read the auto-merged files that both branches touched (`jobs/__init__.py`, `jobs/handler.py`, `job_execution/actions/post.py`, `model/__init__.py`, `celery/tasks.py`). The after-commit email hooks sit next to 26.1's `touch_collections_update_time()` in the commit that finishes the job. 26.1 has the same `ActionBox` call sites as 26.0, plus PickValue's `execute_on_mapped_over`, which doesn't involve `EmailAction`.

## Verification

- `tox -e lint,format,mypy`: OK
- Unit: `test/unit/job_execution/test_email_action.py` (11 passed), `test/unit/app/jobs/test_job_wrapper_finish.py` (10), `test/unit/app/jobs/test_job_wrapper.py` (6), `test/unit/workflows/test_modules.py` (102)
- Integration: `test/integration/test_job_completion_emails.py` (2 passed)

## License
- [x] I agree to license these and all my past contributions to the core galaxy codebase under the [MIT license](https://opensource.org/licenses/MIT).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `490e69352b0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.