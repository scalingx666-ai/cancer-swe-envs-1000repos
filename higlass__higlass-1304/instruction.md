# Issue

**Title:** Fix zoomedY not firing with mouse wheel

## Description

## Summary

- Check `event.sourceEvent?.shiftKey` directly in `zoomed` so value-scale zoom triggers even when Shift is pressed after a gesture has started (the cached `valueScaleZooming` flag is only set at gesture start via `zoomStarted`)
- Fall back to `deltaX` when `deltaY` is zero in `valueScaleZoom`, handling the macOS behaviour where Shift+scroll with a physical mouse wheel converts vertical scroll to horizontal

## Test plan

- [ ] Hold Shift and scroll over a 1d-horizontal track with a **trackpad** — value scale should zoom as before
- [ ] Hold Shift and scroll over a 1d-horizontal track with a **mouse wheel** — value scale should now zoom
- [ ] Confirm regular pan/zoom (no Shift) is unaffected for both input devices

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46eb35683c25`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.