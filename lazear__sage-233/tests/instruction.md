# Issue

**Title:** Support per-mod variable modification limits

## Description

## Summary

Adds optional per-modification occurrence limits and a cap on the total number
of variable-modification combinations generated for each peptide.

This implements the structured variable-modification format proposed in #231:

```json
"variable_mods": {
  "M": [
    {
      "mass": 15.9949,
      "max_count": 1
    }
  ]
}
```

Bare mass values remain supported for backward compatibility:

```json
"variable_mods": {
  "M": [15.9949]
}
```

The two formats can also be mixed within the same configuration.

## Changes

- Add structured variable-modification entries containing `mass` and optional `max_count`
- Add optional database-level `max_combinations`
- Preserve the existing `max_variable_mods` behavior
- Prefer variants with fewer modifications when applying the combination cap
- Preserve structured entries when serializing parameters to `results.json`
- Update documentation and changelog
- Add tests covering parsing, compatibility, limits, caps, and edge cases

`max_combinations` includes the unmodified peptide. A value of `0` is normalized
to `1`, matching the existing behavior of `max_variable_mods`.

Names, labile modifications, and neutral-loss configuration are intentionally
left for future work.

## Backward compatibility

Existing configurations using arrays of numeric masses continue to deserialize
and behave as before. When omitted:

- `max_count` remains unlimited
- `max_combinations` remains unlimited
- `max_variable_mods` retains its existing default and behavior

## Validation

- `cargo fmt --all -- --check`
- `cargo check --workspace --all-targets`
- `cargo test --workspace` — 108 tests passed
- Release build
- End-to-end CLI searches using both structured and legacy configurations
- Verified structured configuration round-trips through `results.json`

Addresses #231.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d74024df7740`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.