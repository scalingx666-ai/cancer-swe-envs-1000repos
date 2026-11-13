# Issue

**Title:** fix(omics-target-evidence-mapper): write the reproducibility bundle with the shared helpers

## Description

## Summary

omics-target-evidence-mapper wrote `environment.yml` and checksums but no `commands.sh`, so it was listed in `skills/contract_known_gaps.json` for `repro_files`. It now writes `commands.sh` through the shared helper and leaves the known-gaps list. The hand-made bundle files at the skill's top level, which were out of date, are deleted.

```diff
 main()
   write evidence.json, report.md, metadata.json, environment.yml, ro-crate-metadata.json
+  write_portable_commands_sh   --demo | --gene/--disease, --max-papers, --max-trials, --output "$OUTPUT_DIR"
   write_checksums              everything above
+                               + commands.sh
```

```diff
 skills/omics-target-evidence-mapper/
-├── commands.sh         # --output demo_out, relative to wherever you ran it
-├── environment.yml     # python=3.11
 ├── SKILL.md            # + Output Structure, commands.sh documented
 └── omics_target_evidence_mapper.py
```

Nothing references the deleted files by path. CI's per-skill environment job only reads `skills/<skill>/environment.yml` for skills with a `tests/*.sh` harness, and this skill has none. `commands.sh` carries a comment that a replay queries live APIs, so results may differ.

## Evidence

- **Before:** `reproducibility/` holds `environment.yml` and `checksums.sha256` (5 entries); no `commands.sh`.
  **After:**
  ```text
  $ python skills/omics-target-evidence-mapper/omics_target_evidence_mapper.py --demo --output <tmp>/out   # exit 0
  $ cd / && PYTHON=<venv python> bash <tmp>/out/reproducibility/commands.sh      # exit 0
  $ cd <tmp>/out && shasum -a 256 -c reproducibility/checksums.sha256
  6 files: OK
  ```
- New `tests/test_repro_bundle.py`: the bundle verifies from the output folder, and `commands.sh` uses `$CLAWBIO_ROOT`/`$OUTPUT_DIR`.
- `skills/omics-target-evidence-mapper/tests` + `tests/`: 498 passed, 2 skipped, 2 xfailed. `generate_catalog.py`: no diff.

Made with `scripts/factory/run.sh repro-bundle omics-target-evidence-mapper` (a separate review agent found nothing it could reproduce), then I reviewed it, rebased it onto main and deleted the stale files.

## Merge Danger

**Door:** two-way

Revert restores the old bundle code and the known-gaps entry.

**Blast Radius:** skill

This and the other repro-bundle PRs (#778, #779, #780 and the five opened alongside this one) each delete one entry from `skills/contract_known_gaps.json`. Whichever merges later may need a one-line rebase there.

---

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4a8c7281c8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.