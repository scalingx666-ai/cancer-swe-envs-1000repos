# Issue

**Title:** Fix review saving, sign-in cancel, chat code blocks and other UI issues

## Description

## Summary
Fixes on top of `main` for issues confirmed against the current code. The cell review part is ported from `Yuxuan/open-ui-vitest` (review files only); the rest is new.

### Review
- **Cell review**: Esc / X / click outside now save staged labels, like the Close button (before, only Close saved). Switching class saves once instead of re-posting `save_annotation/batch` repeatedly, and Yes answers are counted under the class they were made for. Stale tile replies are dropped, staged removals no longer carry over to another slide, a failed first load shows its error instead of a skeleton, Y/N are ignored while typing, and N opens the class picker.
- **Patch review**: closing by any route saves staged labels (same rule as cell review).
- **Patch Classification panel**: class rows can be selected (`onSelect` was never called), so Review opens the chosen class instead of always the first one.

### Sign-in (Electron)
- Closing the sign-in dialog, or starting another sign-in, cancels the pending Google attempt. Before, an abandoned attempt kept its loopback port and raised `OAuth timeout` five minutes later (a full-screen runtime error in dev).
- A real timeout is now an info toast. New `google-oauth-cancel` IPC, registered in both `main.js` and `main_electron.js`.

### Agent chat
- Every fenced code block in a reply is rendered in order with its surrounding text. Before, only the text before the first block and the first block were shown. The text sent as history was always complete, so this is display only.
- New agent avatar (`public/brand/agent_avatar.png`).

### Viewer shortcuts and inputs
- Settings list the **Lasso** shortcut and follow the toolbar's left-to-right order.
- Bindings are saved only on an explicit change or reset. Before, saving on every `bindings` change wrote defaults on mount; with several consumers mounting together, custom shortcuts were reset on reload.
- Prompt fields: Space goes in at the caret and leaves read-only fields alone. Before, it was appended to the end.

### File manager
- A task whose record is gone (`code: 404` envelope or HTTP 404) stops polling at once instead of waiting for the 5-minute timeout. Delete, compress and extract then refresh the folder and say the task may have finished.
- Compress and extract errors replace their loading toast instead of leaving it spinning.
- `imageType` fallback had an operator-precedence bug. The value is not read by the UI today, so this only fixes the stored value.

### Community
- A failed classifier delete keeps the card and shows an error. Before, it warned but removed the card anyway, so it looked deleted while still public.
- An envelope 404 (`code: 404`) counts as already deleted, as a transport 404 already did.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d87c6402f2a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.