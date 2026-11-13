# Issue

**Title:** fix: maintain loading indicator until all DICOM images are loaded

## Description

Maintain Loading Indicator Until All DICOM Images Are Loaded

## Description
This PR fixes an issue where the "Loading images..." status indicator would disappear prematurely before all DICOM instances in a study were fully loaded. The indicator now stays visible throughout the entire loading process, providing users with continuous feedback until all images are available for viewing.

## Problem
Previously, the `hideDicomStatus()` function was being called after each individual DICOM instance was loaded, causing the loading indicator to flash or disappear entirely while the system was still processing remaining images. This created a confusing user experience where users couldn't tell if the loading process was still ongoing or had completed.

## Solution
- Removed `hideDicomStatus()` calls from individual loading functions (`wadorsLoader2` and `loadDICOMFromUrl`)
- Modified `LoadFileInBatches.finishOne()` to only hide the status indicator when all fetches are complete AND the queue is empty
- Ensured proper status display through the entire loading workflow

## Changes Made
- Refactored loading status management in `viewer.js`
- Added condition to only hide status when `NumOfFetchs === 0 && queue.length === 0`
- Maintained existing error display functionality

## Testing Performed
- Tested with studies containing multiple series and instances
- Verified loading indicator remains visible throughout the entire loading process
- Confirmed indicator correctly disappears when loading is genuinely complete
- Validated error messages still display properly when loading fails

## Screen Recording
https://github.com/user-attachments/assets/5e3c635a-f1a5-498e-bf8b-bbc9bae96e33

## Related Issues
Resolves issue with intermittent loading status display.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecd135de15c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.