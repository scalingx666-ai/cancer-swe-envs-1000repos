# Issue

**Title:** fix opensearch deploy followups

## Description

## Issue Number

N/A

## Purpose/Implementation Notes

This pull request introduces several improvements and fixes across deployment scripts, infrastructure configuration, and API responses. The main themes are infrastructure consistency, deployment reliability, and API response normalization.

**Infrastructure and Deployment Consistency:**

* Standardized the OpenSearch domain name from `es-` to `os-` across all relevant Terraform resources, IAM policies, and tags in `infrastructure/instances.tf`, ensuring naming consistency and future-proofing. [[1]](diffhunk://#diff-898bf761c5e755bca8d66f284eb8b124dbdafa5fcd9a32b285ed779cb9667e2cL33-R33) [[2]](diffhunk://#diff-898bf761c5e755bca8d66f284eb8b124dbdafa5fcd9a32b285ed779cb9667e2cL74-R71) [[3]](diffhunk://#diff-898bf761c5e755bca8d66f284eb8b124dbdafa5fcd9a32b285ed779cb9667e2cL89-R87)
* Added `user_data_replace_on_change = true` to EC2 instance resources (`aws_instance.api_server_1` and `aws_instance.foreman_server_1`) in `infrastructure/instances.tf` so that changes to user data scripts trigger instance replacement, ensuring configuration updates are reliably applied. [[1]](diffhunk://#diff-898bf761c5e755bca8d66f284eb8b124dbdafa5fcd9a32b285ed779cb9667e2cR115-R120) [[2]](diffhunk://#diff-898bf761c5e755bca8d66f284eb8b124dbdafa5fcd9a32b285ed779cb9667e2cR189-R193)

**Deployment Script and Static Files Handling:**

* Updated `api/collect_and_run_uwsgi.sh` to clear static files before collecting new ones and removed the explicit HTTP port from the `uwsgi` command, improving static file management and flexibility.
* Removed the unused `STATICFILES_DIRS` setting from `api/data_refinery_api/settings.py` for cleaner configuration.

**API Response Normalization:**

* Updated `_hit_to_dict` in `api/data_refinery_api/views/experiment_document.py` to always set list-typed fields to an empty list when absent, ensuring clients can reliably expect array types and improving compatibility with previous serializers.

## Types of changes

What types of changes does your code introduce?

- Bugfix (non-breaking change which fixes an issue)

## Functional tests

N/A

## Checklist

- [x] Lint and unit tests pass locally with my changes

## Screenshots

N/A

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cfe10ff8700d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.