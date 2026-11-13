# Issue

**Title:** Don't abort the host process on a failed decode: translate C++ exceptions in the Python bindings

## Description

## Problem

When a pixel-data decode allocation fails under memory pressure, GDCM throws a C++ exception out of `Bitmap::GetBuffer`, and through the SWIG Python bindings this becomes an **uncatchable process `abort()` (SIGABRT)** — a single under-memory frame kills the whole interpreter (in a batch/Apache Beam pipeline, the entire worker and everything else it was processing). No Python `try/except` can intercept it.

It is version-independent: on GDCM ≤ 3.0.22 the escaping exception is `std::bad_alloc`; on 3.2.x it is a `gdcm::Exception` from the throwing assert at `gdcmBitmap.cxx:896` (`gdcm_assert(len <= outbv->GetLength())`). The reason it escapes is that the Python interface (`Wrapping/Python/gdcmswig.i`) only wraps a single method (`%exception ReadFooBar`); there is **no global `%exception`**, so the throw crosses the generated `extern "C"` wrapper uncaught → `std::terminate()` → `abort()`.

Full root-cause analysis and a self-contained, runnable reproduction (LD_PRELOAD malloc fault-injection on a synthetic JPEG 2000 frame; baseline decodes, the failing band aborts with exit 134) are here: **

For contrast, `pylibjpeg-openjpeg` decoding the same frame under identical strain raises a catchable Python `MemoryError`.

## Changes

1. **`Wrapping/Python/gdcmswig.i` — global `%exception`.** Translate any uncaught C++ exception escaping a wrapped method into a Python exception (`std::bad_alloc` → `MemoryError`; `std::exception`, which includes `gdcm::Exception`, → `RuntimeError`; `...` → `RuntimeError`). Declared before the class `%include`s so it covers `Bitmap`/`Image`/`Pixmap` decode and everything after. This guarantees no wrapped GDCM method can abort the host interpreter. (`<new>`/`<exception>` added to the `%{ %}` block for the catch types.)

2. **`Bitmap::TryJPEG2000Codec` — graceful decode failure.** A missing or short decoded buffer is a runtime condition (e.g. an allocation failed while decoding), not a logic invariant, so it should not be a throwing `gdcm_assert`. Return `false` instead — `GetBufferInternal` already treats `false` as "couldn't decode", so callers get a normal failure rather than a crash. (The sibling `TryJPEGCodec`/`TryJPEGLSCodec`/`TryRAWCodec` share the same `gdcm_assert(len <= outbv->GetLength())` pattern; happy to extend the same change to them if you'd prefer — the global `%exception` already prevents them from aborting.)

Change 1 is the comprehensive safety net; change 2 fixes the JPEG 2000 path at the source. The Java/C# wrappers have the same `%exception ReadFooBar`-only pattern and would benefit from the analogous global handler, but I've scoped this PR to Python where the issue was reported.

## Verification

The crash and the contrast with pylibjpeg are reproduced and documented in the linked issue. I have **not** built GDCM from source for this patch (no local SWIG/CMake toolchain), so I'd appreciate a CI/maintainer build check — the changes are small and use the standard SWIG `%exception` + `SWIG_fail` idiom already present in this file (`SWIG_exception_fail`) and the existing `catch (std::exception &)` in `ReadFooBar`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0af7384df968`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.