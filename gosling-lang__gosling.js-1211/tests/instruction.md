# Issue

**Title:** fix: prevent axis crash when a narrow view starts at a chromosome boundary

## Description

## Bug
A linear genomic x-axis that is 400px wide or narrower crashes with `Error: invalid format: ,.NaN` when the view starts at the beginning of a chromosome (e.g., `xDomain: { chromosome: 'chr1' }` or a whole-genome view).

At that width the axis shows only two labels, one at each end. The left label's position is `0`, and `formatTick` calls `precisionPrefix(0, viewWidth)`. With d3-format 3.1.2, that returns `NaN` (3.1.0 returned `6`), so `formatPrefix(',.NaN', …)` throws. The formatter is built even when `tickFormat` is `'plain'`, so plain-format axes crash too.

`d3-format` is declared as `^3.1.0`, so apps that install gosling.js fresh resolve 3.1.2 and hit this. This repo's lockfile pins 3.1.0, which is why it doesn't reproduce in the editor here.

## Change List
 - In `formatTick` (`src/tracks/genomic-axis/axis-track.ts`), fall back to a precision of `0` when `precisionPrefix` returns `NaN`.
 - Add `src/tracks/genomic-axis/axis-track.test.ts`. It mocks `precisionPrefix` to return `NaN` for `0`, simulating d3-format 3.1.2, and checks that a label at position 0 formats as `0` (plain) or `0M` (SI), and that other positions are unchanged.

## How to test
 - **Unit test:** run `pnpm vitest run src/tracks/genomic-axis/axis-track.test.ts`. It passes with this change. Reverting `axis-track.ts` makes it fail with `invalid format: ,.NaN`.
 - **In the editor:**
   1. Run `pnpm add d3-format@3.1.2` to match what downstream apps resolve, then `pnpm start`.
   2. Load a spec with one linear track, `"width": 400`, an x-axis, and `"xDomain": { "chromosome": "chr1" }`.
   3. On `v2` this throws `invalid format: ,.NaN`. With this change, the axis renders, and the left label reads `chr1: 0`, or `chr1: 0M` at 200px or narrower, where the axis switches to SI labels.
   4. Revert the `d3-format` change afterwards.

## Checklist
 - [ ] Ensure the PR works with all demos on the online editor
 - [x] Unit tests added or updated
 - [ ] Examples added or updated
 - [ ] [Documentation](https://github.com/gosling-lang/gosling-website) updated (e.g., added API functions)
 - [ ] Screenshots for visual changes (e.g., new encoding support or UI change on Editor)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80d1cf3801ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.