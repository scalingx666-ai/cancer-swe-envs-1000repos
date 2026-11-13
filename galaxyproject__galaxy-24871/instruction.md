# Issue

**Title:** [26.2] Merge release_26.1 into release_26.2

## Description

Merges `release_26.1` (with the `release_26.0` merge from #24870) into `release_26.2`. Based on the 26.0 → 26.1 merge, so merge that one first.

## PRs brought in

- #24835 Send one summary email for jobs mapped over a collection (through the 26.1 hop)
- #24863 Don't leak workflow step database id in dataset_failed messages
- #24826 Fall back to default extension for discovered files without an ext match

## Conflicts

- `lib/galaxy/jobs/handler.py`: 26.2 moved the ready-job query into `_select_ready_jobs()` (per-user sweep cursors). Kept that and added #24835's `settled_jobs` list next to `next_ready_job_cursors`. `__filter_jobs_with_invalid_input_states` takes the new `paused_jobs` argument.
- `lib/galaxy/job_execution/actions/post.py`: kept both import sets (26.2's `DatasetInstance`/HDA/HDCA plus `Job`) and both module constants (`RENAME_INPUT_REFERENCE_PATTERN`, `MAPPED_OVER_SETTLED_STATES`). The new `EmailAction` helpers use `str | None`. `EmailAction` keeps 26.2's default `supports_mapped_over = False`.
- `lib/galaxy/util/unittest_utils/__init__.py`: kept 26.2's `raise_skip_if_site_down` and the incoming `read_mock_emails` (as `str | Path -> list[dict[str, Any]]`).
- `test/unit/app/jobs/test_job_wrapper_finish.py`: 26.2 types these config options, so the 26.1 `cast(Any, self.app.config)` is gone. The test sets `galaxy_infrastructure_url` and `smtp_server` on `self.app.config` directly.
- `lib/galaxy/schema/invocation.py`: `Optional[int]` vs `int | None` only.

## Verification

- `tox -e lint,format,mypy`: OK
- Unit: `test_email_action.py` (11), `test_job_wrapper_finish.py` (11), `test_job_context.py` (9), `test_job_wrapper.py` (18), `test_modules.py` (123), `test_handler.py` (6 passed; its PostgreSQL-only tests were skipped locally)
- Integration: `test/integration/test_job_completion_emails.py` (2 passed)
- API: `test_workflows.py::TestWorkflowsApi::test_workflow_failed_parameter_input_not_ok` (passed)

## License
- [x] I agree to license these and all my past contributions to the core galaxy codebase under the [MIT license](https://opensource.org/licenses/MIT).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1dfcda696ec4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.