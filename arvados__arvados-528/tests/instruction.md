# Issue

**Title:** 526: Update Webpack and related dependencies

## Description

`526-update-webpack-and-related-dependencies` @ e7b8286afc9c649b2232a0c3ed6f26df3431f625

https://ci.arvados.org/job/developer-run-tests/5192/

* All agreed upon points are implemented / addressed.  Describe changes from pre-implementation design.
  * `webpack-dev-server@^5.0.0`
    * Config files and scripts updated following the [migration guide](https://github.com/webpack/webpack-dev-server/blob/master/migration-v5.md).
  * Webpack 5.109.2
    * Further intervention needed if we want to upgrade to the most recent version without warning messages about imports.
  * Webpack plugins including `@pmmmwh/react-refresh-webpack-plugin@^0.6.3`, `webpack-manifest-plugin@^6.0.0`, and `workbox-webpack-plugin@^7.4.1`
  * Non-webpack dependencies updated
    * Applied `update-browserslist-db` for recent browser data
    * Updated DOMPurify to 3.4.15.
* Anything not implemented (discovered or discussed during work) has a follow-up story.
  * _N/A_
* Code is tested and passing, both automated and manual, what manual testing was done is described.
  * Manual tests: ran `yarn start` and `make build` to check that all is well.
* The tested code incorporates recent main branch changes.
  * _Yes_
* New or changed UI/UX has gotten feedback from stakeholders.
  * _N/A_
* Documentation has been updated.
  * _N/A_
* Behaves appropriately at the intended scale (describe intended scale).
  * _N/A_
* Considered backwards and forwards compatibility issues between client and server.
  * _N/A_
* Follows our [coding standards](https://github.com/arvados/arvados/blob/main/doc/development/CodingStandards.md) and [GUI style guidelines](https://github.com/arvados/arvados/blob/main/doc/development/CodingStandards.md#workbench-design-guidelines)
  * _Yes_

This also addresses dependabot PR #461. Note that we can't update to webpack-dev-server 6, because it dropped support for NodeJS 20.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d93141dbac11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.