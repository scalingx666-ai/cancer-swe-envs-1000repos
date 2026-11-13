# Issue

**Title:** Added the app_context wrapper

## Description

Hi @pchlap,

Thank you again for your time earlier.

When running the DIRQA service from RayStation we encountered an error in the series_received workflow:
```
2026-03-12 22:49:35,873 - pynetdicom.events - ERROR - Exception raised in user's 'evt.EVT_RELEASED' event handler 'on_association_released'
2026-03-12 22:49:35,873 - pynetdicom.events - ERROR - Working outside of application context.
```
This occurred because the `on_association_released` event handler was executed outside of the Flask application context.

The issue has been resolved by wrapping the relevant code block in `app.app_context()` so that the handler runs within the correct application context.

The fix was tested on several datasets and resolved the issue as expected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1168be11628`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.