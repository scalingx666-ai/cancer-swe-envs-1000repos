# Issue

**Title:** perf(core): faster start and load of a large streaming volume

## Description

## What this pull request does

This pull request makes the start time and the load rate of a large volume faster. It is a
, which added the multi-resolution volume textures and shipped in release
5.17.0. The branch is release 5.17.0 plus seven commits. It changes no public API.

OHIF/Viewers#6295 builds its CI and its Netlify deploy preview against this branch, with the
line `CS3D_REF: perf/fidelity-notification-incremental`. When this pull request merges and a
release holds it, OHIF/Viewers#6295 removes that line and pins the release.

## Changes

### `9e3514e1a`: coalesce the fidelity notifications, and keep the delivery coverage incremental

Before this commit, a streaming volume calculated the fidelity state once for each image that
arrived. Each calculation built the coverage of all of the earlier deliveries again. Thus the
cost of a load increased with the square of the number of images.

- `BaseVolumeViewport` sends the fidelity notification for `IMAGE_VOLUME_MODIFIED` at most once
  for each animation frame. `IMAGE_VOLUME_LOADING_COMPLETED` and the render path still send the
  notification at once.
- `CompositeVoxelManager` keeps sorted k bounds in the delivery index. It also keeps the merged
  runs of the best quality for each i, j footprint, and it does this for the deliveries that it
  maps into a derived grid too.
- A query reads the runs inside the region. For several footprints, or when the full count can
  be an estimate, the query uses the full calculation. Thus the records are the same as before.
- `packages/docs/docs/specs/core/viewport-fidelity.md` records the rule of one notification for
  each animation frame.

### `03dce34d7`: skip the zero upload of a slice that new texture storage never received

New texture storage reads 0. Thus a slice with no data uploads nothing, until a slice with data
is written to that position. The texture keeps one flag for each slice of the allocation, and
`create3DFromRaw` resets the flags. A slice that held data before still uploads the cleared slab,
for example after the volume resets its composite. A skipped slice uses none of the fill budget.

### `10d8426ff`: start the clear of new volume texture storage early, and wait on a fence

A browser allocates `texStorage3D` storage only when the storage is first used, and then it
clears the whole level. For a large volume, the first slice uploads then block the main thread
for some seconds.

- After the allocation, the texture sends one 1x1x1 upload to start the clear. It then adds a
  fence and calls a flush.
- A timer reads the state of the fence, and does not block the thread.
- Until the fence signals, the texture skips its uploads. Both streaming mappers skip the draw
  of the actor, so no draw reads the texture before a readback of the shared context.
- When the fence signals, the texture renders the viewports of its volume again.
- A lost context counts as a signalled fence. A new allocation replaces the fence. Without the
  fences of WebGL2, the behaviour does not change.

### Review fixes: `8c0c52f5f`, `2c6912ada`, `1f89ea606`, `85cac5f1e`

The first version of the fence failed two Karma tests:
`BidirectionalTool` "modify its handle" and `CircleROIStartEnd` "512 x 128". The cause was
the empty frame. A volume viewport rendered twice: the first render drew nothing, but it still
fired `IMAGE_RENDERED`. A test that acts on each `IMAGE_RENDERED` acted twice, or acted on
a viewport that a later test had destroyed.

- **The fence applies only to a large texture.** The limit is 256 MB of storage
  (`INIT_FENCE_MIN_BYTES`). A 256³ int16 texture (32 MB) clears in about 30 ms. Below the
  limit, the texture uses the path of 5.17.0: no 1 × 1 × 1 upload, no fence, and no skipped
  draw.
- **The engine fires no event for the empty frame.** The mappers record the time of each
  skipped draw. `ContextPoolRenderingEngine` and `TiledRenderingEngine` fire no
  `IMAGE_RENDERED` and no fidelity event for a viewport in which no actor drew in that render.
  When another actor drew, for example a small PET over a waiting CT, the engine fires the
  events, so the annotations follow the camera.
  The render after the fence signals fires the events. The record holds the skip, not the
  state of the fence, so a fence that signals during the render cannot let the empty frame
  through.
- **The poll stops with the texture.** `releaseGraphicsResources` and `delete` cancel the
  timer of the poll. A poll of a deleted texture or of a replaced fence does nothing.
- **The wait has a deadline.** After 3 s (`INIT_FENCE_DEADLINE_MS`), the texture stops the
  wait and uses the blocking path. The measured clear takes 150–300 ms.
- **Docs:** FIDELITY-EVENT-4 states the new event rules. Items 12 and 13 of the 5.x migration
  notes give the fewer fidelity events of a load and the blank first frame of a large volume.
- **Tests:** two engine tests check that an empty frame withholds the events, and that a drawn
  actor in the same viewport keeps them. Four new tests go through `create3DFromRaw({ data: null })`. They cover the fence
  above the limit, no fence below the limit, the deadline, and the cancel of the poll on
  `delete`. The coalescing test cleans up in `finally`.

Karma passes with the limit set to 0, so that every volume texture uses the fence: the tools
set passes 108 of 108. With the real limit, the full suite passes 253 of 253. Jest passes 1212
tests, and `tsc` gives no errors.

## Measured results

OHIF production build, `config/netlify.js` (final downsampling on), the preset `high`, the
2464-image CT (512 × 512) in the MPR layout of three viewports. Chromium on Windows 11 with an
Intel UHD GPU (ANGLE D3D11). One run for each cell.

| | 5.17.0 cold / warm | This PR cold / warm |
| --- | --- | --- |
| Main thread blocked before the first image is processed | 2.3 s / 2.3 s | 0.12 s / 0.12 s |
| Shader compile | 1.6 s / 1.6 s | 0.05 s / 0.06 s |
| First image (OHIF timer) | 3.8 s / 3.7 s | 1.9 s / 1.9 s |
| Images per second, 15–35 s | 4.5 / 5.0 | 88 / 74 |
| Main thread in the fidelity chain | 84% / 83% | 1% / 1% |
| All 2464 images loaded | not reached after 70 s | 34 s / 26 s |

- On 5.17.0 the first slice uploads and the shader compile wait for the clear of the texture in
  the GPU process. The trace shows the main thread in `CommandBufferProxyImpl::WaitForToken`
  and in `GetShaderiv`. On the deploy preview, the same wait took 6.5–7.2 s.
- With a texture edge of 256 (`low-tablet`), 5.17.0 blocks for less than 1 s. Thus the size of
  the texture is the cause of the wait.
- The trace of this PR has no `WaitForToken` on the main thread, and no readback that waits.
  The GPU process clears the texture in about 150–300 ms, in parallel with the network. The
  shader compile is fast, because it no longer waits behind the clear.
- A unit benchmark of the coverage (2464 deliveries in the coarse interleaved order, one query
  after each delivery) went from 17,492 ms to 783 ms.
- The next hot spot of the load is `fillPlaneByAverage`, at about half of the busy time.

## Changes that an application can see

- An application that counts `VIEWPORT_FIDELITY_CHANGED` events during a load gets fewer
  events: at most one for each animation frame, not one for each image. The last state is the
  same. The built-in indicator reads only the last state.
- A volume event that no render follows reaches the listeners up to one frame later.
- A new volume viewport with more than 256 MB of texture storage stays blank for about 0.3 s,
  while the browser clears the texture. A blank viewport is obvious to the user, so the fidelity
  indicator shows no pending state.
- For a frame in which no actor of the viewport drew, the engine fires no `IMAGE_RENDERED` and
  no fidelity event. The first
  `IMAGE_RENDERED` of the viewport comes with the first frame that shows the volume. A smaller
  volume behaves as in 5.17.0.
- The spec change of FIDELITY-EVENT-7 in `viewport-fidelity.md` describes the implementation,
  not a user requirement. A maintainer can move the text to an implementation specification.

## Known limits

- An oblique derived grid, where the mapped footprint changes along k, uses the full
  calculation. The result is correct, but the cost does not change.
- The Safari path of vtk.js that uses `texImage3D` in place of `texStorage3D` was not tested.
- All measurements come from one Intel integrated GPU. A discrete GPU can give different times.

## Tests

- `npx jest` in `packages/core`: 84 suites pass (1207 tests, 2 skipped).
  `npx tsc -p packages/core/tsconfig.json --noEmit` gives no errors.

- `packages/core/test/fidelityIndicatorAttach.jest.js`: a burst of `IMAGE_VOLUME_MODIFIED`
  events gives one notification.
- `packages/core/test/utilities/CompositeVoxelManager.jest.js`: a new group of tests for the
  incremental coverage of the deliveries.
- `packages/core/test/vtkStreamingOpenGLTexture.jest.js`: the texture skips the zero upload of an
  empty slice, and waits for the fence before its uploads.

## How to test

Open the OHIF deploy preview of OHIF/Viewers#6295, which uses this branch. Load the 2464-image CT
`Body 0.5 CE` in the MPR layout:

https://deploy-preview-6295--ohif-dev.netlify.app/viewer?StudyInstanceUIDs=1.3.6.1.4.1.14519.5.2.1.99.1071.24993177073256607564948872275593&hangingProtocolId=mpr&customization=gpu/high

The preview selects the preset `medium` by default. The `gpu/high` customization in the link gives
the largest texture, which shows the start time most clearly.

- The first images show sooner than on release 5.17.0, and the main thread does not stop for
  some seconds at the start of the load.
- All 2464 images load in about 30 s. On release 5.17.0, fewer than half of the images load in
  70 s.
- The fidelity indicator shows the same states as on release 5.17.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Progressive volume rendering avoids drawing with textures that are still initializing, reducing incomplete images.
  * Volume updates skip untouched empty slices while still clearing slices that previously contained data.
  * Fidelity updates during bursts of image changes are sent at most once per frame, after the frame’s final event.
  * Render-complete and fidelity notifications are withheld when a viewport has no actor ready to draw.

* **Performance**
  * Large GPU textures can initialize asynchronously where supported.
  * Composite-volume coverage queries, including queries on derived grids, are more efficient.

* **Documentation**
  * Migration notes describe changes to progressive loading and large-texture rendering.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86c01e417829`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.