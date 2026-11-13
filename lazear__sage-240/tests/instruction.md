# Issue

**Title:** chore: migrate sage-cloudpath to reqwest 0.12

## Description

## Summary
- Bump `reqwest` in `sage-cloudpath` from 0.11 (`rustls-tls`) to 0.12 (`rustls-tls-native-roots`). The features match what `object_store` already enables, so both share one TLS stack.
- Removes `webpki-roots 0.25.4`, a 2023 root bundle that includes eMudhra's emSign roots, along with the duplicate rustls 0.21 / hyper-rustls 0.24 / reqwest 0.11 tree (about 377 lines removed from `Cargo.lock`).
- `send_data` compiles unchanged on 0.12.

## Notes
- HTTPS now trusts the OS certificate store, so the eMudhra intermediate exposure ends once distro CA bundles drop or distrust those roots. No further sage change is needed for that.
- The Docker image already installs `ca-certificates`.

## Testing
- `cargo build --release`
- `cargo test -p sage-cloudpath` passes (18 tests)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb9934ff4820`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.