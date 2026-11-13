# Issue

**Title:** 524: WB: Sanitize resource description displayed in <td> with DOMPurify

## Description

`524-table-cell-content-render` @ 6a0c5ce7ee0e6e1a2cfa79eb134109cac59e2190

https://ci.arvados.org/job/developer-run-tests/5185/

* All agreed upon points are implemented / addressed.  Describe changes from pre-implementation design.
  * The goal is to display a resource description in a table cell. The previous approach used a regular expression to look for `<p>` and `</p>` and remove them. This wouldn't work if the element has attributes (and some attributes are allowed). (Notice that our rich editor by default creates text that is wrapped in `<p>` tags.)
  * We already use the `DOMPurify` library to sanitize all `description` fields of resources, so here we use it again, with a restricted set of configs more suitable for table display. Namely, we only allow inline elements (not including the inline-block `<img>` element) and disallow `<p>`. Custom styling (`style` attribute) is disallowed too, and the allowed attributes only cover what the allow-listed elements to work.
* Anything not implemented (discovered or discussed during work) has a follow-up story.
  * _N/A_
* Code is tested and passing, both automated and manual, what manual testing was done is described.
  * A new component test is added for the routine `RenderDescriptionInTD`.
  * Manual testing with visual and devtools inspections of the resulting live page.
* The tested code incorporates recent main branch changes.
  * _Yes_
* New or changed UI/UX has gotten feedback from stakeholders.
  * _N/A_ (I think this is a fairly uncontroversial fix UI-wise)
* Documentation has been updated.
  * _N/A_ (We do have docs for allowed tags: https://doc.arvados.org/main/api/resources.html#descriptions; this PR doesn't change that, only how the description data is further processed for display)
* Behaves appropriately at the intended scale (describe intended scale).
  * _N/A_
* Considered backwards and forwards compatibility issues between client and server.
  * This only affects the display of data.
* Follows our [coding standards](https://github.com/arvados/arvados/blob/main/doc/development/CodingStandards.md) and [GUI style guidelines](https://github.com/arvados/arvados/blob/main/doc/development/CodingStandards.md#workbench-design-guidelines)
  * _Yes_

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d909e69b5579`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.