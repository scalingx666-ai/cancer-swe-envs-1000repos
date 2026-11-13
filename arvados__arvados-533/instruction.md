# Issue

**Title:** 532: Fix labels to the copy-to-clipboard buttons.

## Description

`532-wb-fix-copy-button-label` @ b378ae827597273471536ccfd341ef35f0c7a766

https://ci.arvados.org/job/developer-run-tests/5199/

* All agreed upon points are implemented / addressed.  Describe changes from pre-implementation design.
  * Small copy icon next to values in the details view: "Copy link to clipboard" -> "Copy value to clipboard"
  * "Command" tab in Process view: "Copy command to clipboard". Similarly for Logs tab.
  * "Get API token" page: "Copy link to clipBOARD" -> "Copy code to clipboard" (this is about copying the environment variable exporting code for shell).
* Anything not implemented (discovered or discussed during work) has a follow-up story.
  * _N/A_
* Code is tested and passing, both automated and manual, what manual testing was done is described.
  * Manual testing: in-browser inspections.
* The tested code incorporates recent main branch changes.
  * _Yes_
* New or changed UI/UX has gotten feedback from stakeholders.
  * _N/A_ (it's a tiny change)
* Documentation has been updated.
  * _N/A_
* Behaves appropriately at the intended scale (describe intended scale).
  * _N/A_
* Considered backwards and forwards compatibility issues between client and server.
  * _N/A_
* Follows our [coding standards](https://github.com/arvados/arvados/blob/main/doc/development/CodingStandards.md) and [GUI style guidelines](https://github.com/arvados/arvados/blob/main/doc/development/CodingStandards.md#workbench-design-guidelines)
  * _Yes_

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c7af37cd3c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.