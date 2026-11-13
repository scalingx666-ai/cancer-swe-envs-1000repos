# Issue

**Title:** ci: bump codecov-action to v6.0.2

## Description

Every CI run is currently failing at the `Code Coverage` step, on `main` and on every open PR. The unit tests themselves pass — the most recent run on #1163 reported `Tests: succeeded 1605, failed 0` and then died in the next step, and the other two matrix jobs were fail-fast cancelled mid-suite, which is why all three show red.

## Cause

Codecov deleted the `codecovsecurity` Keybase account. The wrapper bundled with v6.0.0 hardcodes that account when fetching its verification key (`dist/codecov.sh:113`):

```sh
echo "$(curl -s https://keybase.io/codecovsecurity/pgp_keys.asc)" | \
  gpg --no-default-keyring --import
```

That URL now returns `404` with the plain-text body `SELF-SIGNED PUBLIC KEY NOT FOUND`. `curl -s` has no `-f`, so the 404 body is not treated as an error — it is piped into `gpg --import`, which imports nothing, and verification of the uploader binary then fails:

```
gpg: no valid OpenPGP data found.
gpg: Total number processed: 0
gpg: Signature made Thu Jul  9 01:37:57 2026 UTC
gpg:                using RSA key 27034E7FDB850E0BBC2C62FF806BB28AED779869
gpg: Can't check signature: No public key
==> Could not verify signature. Please contact Codecov if problem continues
```

Because we set `fail_ci_if_error: true`, that exits the job non-zero. This will not self-heal on a re-run.

Codecov's own v7.0.0 release notes confirm it: "Due to migration issues with keybase, we are unable to update our keys under the `codecovsecurity` account. We have deleted the account and are using `codecovsecops` with the original gpg key".

## Fix

v6.0.2 fetches the key from the `codecovsecops` account. That account serves the identical key — importing it locally yields fingerprint `27034E7FDB850E0BBC2C62FF806BB28AED779869`, byte-for-byte the key that signed the uploader in the failing logs — so signature verification is genuinely restored, not bypassed. Preferable to `skip_validation: true` or `fail_ci_if_error: false`, which would paper over it and drop the supply-chain check on a 10 MB binary.

v6.0.2 and v7.0.0 are the same commit (`fb8b3582c8e4def4969c97caa2f19720cb33a72f`); the v6.0.2 notes describe it as "a copy of the v7.0.0 release to make updates easier", so there is no behavioral difference between them and no breaking change for our usage. This also picks up the v6.0.1 template-injection fix (VULN-1652).

Pinned by commit SHA per repo convention. Note that the annotated tag `v6.0.2` dereferences to tag object `8cad3ba9…`; `fb8b3582…` is the commit it points at, which is what belongs in `uses:`.

For reference, fgumi is already on this same commit.

## Testing

The proof is this PR's own CI — the `Code Coverage` step should go green. Verified out-of-band that `https://keybase.io/codecovsecops/pgp_keys.asc` returns `200` with a valid PGP block and that the old URL returns `404`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8611404b380e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.