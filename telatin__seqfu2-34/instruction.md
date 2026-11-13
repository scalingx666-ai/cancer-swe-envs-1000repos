# Issue

**Title:** Build/portable release binaries

## Description

## Portable, faster release binaries

Fixes portability problems in the published binaries, removes the runtime PCRE dependency, and makes the build friendlier to packagers such as Bioconda.

### Problems fixed
- **macOS binaries required macOS 15+** (`minos 15.0` in v1.29.0). The build now sets `MACOSX_DEPLOYMENT_TARGET` to 11.0 for arm64 and 10.13 for x86_64.
- **Linux binaries required glibc ≥ 2.34** because they were built on ubuntu-24.04, so they would not run on RHEL/Rocky 8, Ubuntu 20.04, Debian 11 or many HPC systems. They are now built in `manylinux_2_28` containers (glibc 2.28) with a pinned, checksum-verified Nim 2.2.10.
- **Runtime `libpcre` lookup**, pulled in by `tableview`'s `import re`. The new minimum, `tableview >= 0.6.0`, uses the pure-Nim `regex` package, and the binary no longer references PCRE.

### Release workflow (`release-binaries.yml`)
- Builds all tools (`make all`) and runs `test/mini.sh` on every platform before uploading.
- Release assets:
  - `seqfu-<platform>`: the main binary alone, same name as before, so existing download links keep working
  - `seqfu-<version>-<platform>.tar.gz`: all `fu-*` tools, plus LICENSE and README
  - `SHA256SUMS`
- Can also be started by hand (`workflow_dispatch`); a manual run builds and tests but doesn't upload anything. This replaces the duplicate `build-binaries.yml`, which is removed.
- Drops `zlib1g-dev`/`libpcre3-dev` from the release build (gzfast bundles zlib) and removes the no-op `--threads:on` append to `nim.cfg`. `make.yaml` no longer installs `libpcre3-dev`.

### Makefile
- **Faster, smaller binaries**:
  - `-d:lto` is on by default. On Apple Silicon: `seqfu stats` ~20% faster, `seqfu rc` ~4% faster, gzipped input ~5% faster.
  - Stripping is on by default: `seqfu` shrinks from 2.49 to 2.22 MB. Linux uses `-d:strip`; macOS uses `-Wl,-x`, since Apple's ld ignores `-s`.
  - Switches: `LTO=0` and `NIMSTRIP=0` turn these off. `NIMFLAGS=...` passes extra Nim options.
- **Uses the environment's compilers**: `CC`/`CXX` are no longer hard-coded and `CFLAGS`/`CXXFLAGS` use `?=`, so conda's toolchain is used without patching the Makefile with `sed`.
- **Dependency handling**:
  - `src/deps.txt` now depends on `seqfu.nimble`, so dependency bumps are actually installed.
  - Every Nim target depends on it, which makes `make -j` safe.
  - The rule fails when nimble reports a resolution error; nimble itself exits 0 in that case, which let builds silently fall back to an older tableview.

### Other
- `nim.cfg`: documents why `-d:danger` stays. Re-enabling checks costs ~20% on `seqfu rc`.
- `seqfu.nimble`: license corrected from MIT to `GPL-3.0-only`, matching `LICENSE` and Bioconda.
- `fu-split`, `fu-pecheck`: shebang changed to `python3`.

### Testing
- Clean `make -j8 all` on macOS arm64; `bash test/mini.sh`: all 657 tests pass.
- Checked `MACOSX_DEPLOYMENT_TARGET=11.0` → `minos 11.0`.
- Checked the packaging script locally.
- **Not yet run on GitHub:** the manylinux container jobs. Before merging, trigger with
  `gh workflow run release-binaries.yml --ref build/portable-release-binaries`
  and confirm `strings seqfu-linux-x86_64 | grep GLIBC_ | sort -V | tail -1` prints ≤ `GLIBC_2.28`.

### Follow-up
- Update the Bioconda recipe after the next release: drop the `pcre` and `sed` patching, require `nim >=2.2.0`, add `python` as a run dependency, pin the osx-arm64 Nim download.
- Consider adding a `nimble.lock` so builds use fixed dependency versions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c1b4d09e24f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.