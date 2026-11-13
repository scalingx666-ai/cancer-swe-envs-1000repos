# Issue

**Title:** chore(dependencies): upgrade dependencies

## Description

## Summary
- A single DICOM file now opens through a Nextcloud file action, the same path a folder already uses, so the app no longer mounts a component inside the Nextcloud Viewer.
- That removes the Vue 2 requirement. The shell now builds with Vue 3.5.44, `@nextcloud/vue` 9.14.0, and `@nextcloud/dialogs` 8.0.0.
- Nextcloud 33–35 stays supported. Vue 3 lives only in this app’s own scripts. The shipped Viewer app on those versions is still Vue 2, and this app is no longer a child of it.

## Changes
- Register `dicomviewer-file` as the default action for `application/dicom` and `application/dcm`. Clicking the file name opens the study in a new tab.
- The private single-file URL is still `owner|fileid`, with no `|1`. PHP keeps scanning that file’s folder for `application/dicom` files and marks the clicked file as the selected image.
- The folder action is unchanged: `owner|fileid|1`, which also includes files with no DICOM extension.
- Remove `OCA.Viewer.registerHandler` and delete `src/views/DICOMView.vue`.
- Mount the DICOM sidebar with Vue 3 `createApp`. The attribute table is wrapped in `thead` and `tbody`.
- Raise `@nextcloud/auth`, `axios`, `l10n`, and `router` to the versions dialogs 8 needs. Keep the l10n override at 3.4.1.
- Add webpack, vue-loader 17, and the Babel packages as direct dev dependencies, and drop the Vue 2 `prettify` option that vue-loader 17 rejects.
- Keep the `node-forge` 1.4.2 and nested `minimatch` 9.0.9 overrides.

## Audit
`npm audit` on this tree: 0 critical, 0 high, 0 moderate, 6 low. All 6 are the same elliptic advisory (`GHSA-848j-6mx2-7j84`), which matches the elliptic findings already present on current Nextcloud. PostCSS, qs, brace-expansion, vue 2, and vue-template-compiler are gone from this app’s audit.

## Environment
- Nextcloud 35.0.2
- Node 24.21.0 and npm 11.19.0
- Install with `npm install --legacy-peer-deps`. `@nextcloud/webpack-vue-config` 6 still declares a Vue 2 peer, so a normal `npm install` fails with `ERESOLVE`
- Rebuild the shell with `npm run dev`. Do not use `npm run build` for this check; its prebuild step wipes `js/` and rebuilds the OHIF viewer with yarn

## Test plan
- [x] Hard-refresh, then open a DICOM. The name reads “Open with DICOM Viewer” and the study opens
- [x] Details → DICOM tab shows the attribute table and thumbnail.
- [x] A non-DICOM file, such as a PNG or PDF, still uses Nextcloud’s normal View action.
- [x] Public share of one DICOM file: the View link opens that file.
- [x] Public share of a folder: opening one DICOM file loads the folder and shows that file.
- [x] Password-protected share: the viewer loads after the password, and `/publicdicomjson` returns 403 before it.
- [x] Public share with “Hide download” enabled: the Capture tool is hidden. With it disabled, Capture is visible.
- [x] Investigational-use notice appears, and “Confirm and hide” keeps it hidden for 90 days.
- [x] A folder with more than one series: the whole folder loads. The clicked image is selected when it belongs to the series the viewer opens first.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d067ab55c90e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.