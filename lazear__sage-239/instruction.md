# Issue

**Title:** feat: add radical z ions for ETD and ECD

## Description

Adds an opt-in `z_radical` ion type (`y - NH2`) for ETD/ECD. It follows the existing C-terminal indexing and scoring paths, and uses the ASCII label `z_radical` in JSON, TSV, and Parquet. The existing `z` type remains `y - NH3`; default b/y searches are unchanged.

Also corrects the local ammonia mass to `N + H * 3.0`, replacing its proton-containing expression. This corrects the small c, x, and non-radical z mass offsets.

Example configuration override:

```json
{
  "database": {
    "ion_kinds": ["c", "z_radical"]
  }
}
```

Validation:

- `cargo fmt --check` and `cargo test --workspace --locked` pass (121 tests).
- Tests check radical-z masses at charges 1 and 2, the ammonia correction, JSON names, and terminal/internal modifications.
- Local checks on 12 previously identified real spectra (six ETD, six EThcD) recover the expected rank-1 peptide and precursor charge in c-only, z-only, and combined c/z searches, without artificial terminal offsets.
- TSV and Parquet peptide results agree. Exported fragment types, ordinals, and calculated masses were checked independently; the largest mass difference was 0.000404 Da. This selected-spectrum check is not an accuracy benchmark.

Fixes 

AI-assisted PR prepared with Codex, every change manually inspected by @tentrillion (though he is not a Rust person).  

**I instructed Codex to simplify the extra tests it initially proposed and match the style of the codebase, and to revert it's removal of the `NH3` constant to a remote library to match the style of the existing codebase.**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4315a05a32d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.