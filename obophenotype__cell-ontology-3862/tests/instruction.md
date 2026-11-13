# Issue

**Title:** Strip CL axioms from PCL before building cl-plus

## Description

## Problem

`cl-plus.owl` merges the released `pcl-base.owl` into `cl-full.owl` and reasons over the result. `pcl-base.owl` (currently 2025-07-07) also contains copies of CL axioms from the CL release it was built against: 2,587 axioms whose subject is a CL term, including old logical definitions.

When CL changes a definition, cl-plus contains both the old and the new version. With #3841 (MGE- and CGE-derived interneurons) merged, the next release's `cl-plus` step fails:

```
Equivalence: CL_0020125 == CL_4042039
Equivalence: CL_0020124 == CL_4023063
Equivalence: CL_4023064 == CL_0020125
Equivalence: CL_4023064 == CL_4042039
```

Re-releasing PCL doesn't fix this, because PCL builds against released CL, so it would still carry the old definitions.

## Change

`cl-plus` now merges `tmp/pcl-base-no-cl.owl`: `pcl-base.owl` with every axiom whose subject is a CL term removed (`robot remove --base-iri http://purl.obolibrary.org/obo/CL_ --axioms internal`). CL's own axioms then always win.

- Everything else in PCL is kept: PCL classes and their links to CL terms, taxonomy individuals, gene classes and marker sets. I checked this by diffing the axioms. The only ones removed are the 2,587 with a CL subject.
- The filtered file is rebuilt on every run (`.FORCE`), so the latest PCL release is still used.

## Testing

Run with `cl-full.owl` from #3841 plus the updated WMBO component, using the cl-plus recipe's `merge`/`unmerge`/`reason`/`relax`/`reduce` steps:

| PCL input | Result |
|---|---|
| `pcl-base.owl` as released | fails with the four equivalences above |
| filtered (this PR) | passes |

- PCL coverage is unchanged: 21,795 of 22,149 PCL classes have a named parent, both with the released PCL (reasoned with equivalences allowed) and with the filtered one.
- 58 PCL classes get different direct parents, because their CL parents now come from current CL rather than PCL's stale copy. For example, `PCL:0051484` moves from CL:0020124 to CL:4023063, and several PCL classes lose a redundant direct CL:4072029 parent.
- The new target also runs in the ODK container (`make tmp/pcl-base-no-cl.owl`).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `122c0b78013a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.