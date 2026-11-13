# Issue

**Title:** Skip tests when GitLab rate-limits sample data downloads

## Description

## Description

.

Since October 19, 2026, GitLab.com limits unauthenticated traffic to 60
requests per hour per IP address
([announcement](https://about.gitlab.com/blog/rate-limit-change-2026/)). Tests
that download scikit-image sample data from GitLab (`eagle`, `brain`,
`cells3d`, and reference arrays for the rank filter, footprint and restoration
tests) now fail in CI with `429 Too Many Requests`. scikit-image only turns
`ConnectionError` into a skip, so the `HTTPError` raised for a 429 fails the
test, and `test_rank.py`, which fetched its reference data at import time, fails
to collect.

This PR is a workaround that skips these tests when the data cannot be
downloaded, while we decide where else to host the data (about 16 MB in total):

- `fetch()` and a new `load_sample_data()` helper in
  `cucim.skimage._shared.testing` skip the test if the download fails.
- A 429 is not retried. GitLab asks clients to wait until the hourly window
  resets, so pooch's retries 1 to 3 seconds apart cannot succeed. After the
  first 429, later downloads in the session are skipped without a request.
  Other failures (e.g. a dropped connection) are still retried 3 times.
- Data shared by several tests is loaded in module-scoped fixtures, and the
  rank filter reference data is loaded only by the two tests that use it.

With every download returning 429 and an empty cache, the affected tests make
one request in total and skip instead of failing. On `main`, each of these tests
downloads the data itself, with 4 attempts. Tests that don't need the data
still run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9eaff1e6fdf5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.