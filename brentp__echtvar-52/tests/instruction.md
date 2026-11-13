# Issue

**Title:** Add support for Flag field type

## Description

## Summary
- Adds `Flag` variant to `FieldType` enum, enabling VCF INFO fields with `Type=Flag` to be encoded and annotated
- Flags are encoded as u32 values of 0 (absent) or 1 (present), which stream-vbyte compresses to ~1 byte per value
- During annotation, flags are emitted via `push_info_flag` only when present (value=1); absent flags are omitted from the output record
- Sets `missing_value=0` for Flag fields so missing variants correctly result in absent flags

## Test plan
- [x] Unit tests for Flag `FieldType` deserialization from JSON5
- [x] Config roundtrip test (JSON serialize/deserialize as stored in zip config.json)
- [x] Missing value semantics test (verifies 0/1 encoding, not confused with u32::MAX sentinel)
- [x] All 15 existing + new tests pass (`cargo test`)
- [x] Build succeeds with no errors

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53c7518a89e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.