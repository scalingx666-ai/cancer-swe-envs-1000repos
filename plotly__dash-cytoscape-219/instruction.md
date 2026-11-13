# Issue

**Title:** Bugfix/cyleaflet tiles not found

## Description

## About
This PR fixes two bugs in the CyLeaflet all-in-one component:
- #206 
- #218 

## Description of changes 
- #218 fix:
  - `maxZoom` has been added to the default value of `leaflet_children`. The `maxZoom` value can't be increased after the initialisation of the `dash_leaflet` component but it can be reduced. By initialising it with a very high value it's ensured it can be updated.
  - A demo file has been added to test the correct functionality: `demos/usage-cy-leaflet-maxzoom.py`
- #206 fix:
  - The `dash_leaflet` version has been upgraded to `>=1.0.16rc3`. This version includes the fix to round decimal zoom level values, which was causing incorrect requests of tiles. See comment in 
  - A demo file has been added to test the correct functionality: `demos/usage-cy-leaflet-update-tiles.py`

## Pre-Merge checklist
- [x] The project was correctly built with `npm run build:all`.
- [x] If there was any conflict, it was solved correctly.
- [x] All changes were documented in CHANGELOG.md.
- [x] All tests on CircleCI have passed.
- [x] All Percy visual changes have been approved.
- [x] At least one person has :dancer:'d the pull request.


## Reference Issues
 
 

## Other comments
New demo files can be used to test these fixes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a096d968118`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.