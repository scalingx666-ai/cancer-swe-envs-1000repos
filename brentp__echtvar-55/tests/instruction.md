# Issue

**Title:** Update rust-htslib to fix compilation on aarch64 Linux

## Description

Updates `rust-htslib` to apply this fix: https://github.com/rust-bio/rust-htslib/releases/tag/rust-htslib-v0.39.3

Otherwise, compilation fails with many instances of:

```text
error[E0308]: mismatched types
   --> /home/ubuntu/.cargo/registry/src/index.crates.io-1949cf8c6b5b557f/rust-htslib-0.38.2/src/bam/record.rs:152:16
    |
152 |             s: sam_copy.as_ptr() as *mut i8,
    |                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^ expected `*mut u8`, found `*mut i8`
    |
    = note: expected raw pointer `*mut u8`
               found raw pointer `*mut i8`
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23c90dee7daf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.