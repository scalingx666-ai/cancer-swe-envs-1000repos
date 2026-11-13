# Issue

**Title:** feat: allow React 19 as a peer dependency

## Description

## Summary

  `v2` already develops on React 19, but the published peer range stops at React 18, so npm 7+ refuses to install gosling.js into a React 19 app (ERESOLVE). This PR adds React 19 to the range without
  dropping any version. It also types the `ref` prop so React 19 consumers don't need a cast.

  ## Changes

  - **Peer range:** `react` and `react-dom` are now `^16.6.3 || ^17.0.0 || ^18.0.0 || ^19.0.0`. The range only grows, so installs that worked before still work.
  - **`ref` type:** `GoslingComponent`'s `ref` prop is now `Ref<GoslingRef>` instead of `RefObject<GoslingRef>`. Under React 19 types, `useRef<GoslingRef>(null)` returns `RefObject<GoslingRef |
  null>`, which the old type rejected, so callers had to cast. `Ref` also accepts callback refs.
  - **Dev types:** `@types/react` and `@types/react-dom` move to 19. This needed three `useRef()` → `useRef(undefined)` fixes in the editor. These changes are dev-only and don't ship.
  - **Published types:** `GoslingComponent` now declares `ReactElement` as its return type. Built with React 19 types, the inferred type came out as `React.JSX.Element` with a default `React` import.
  That breaks consumers on `@types/react` older than 18.2.7, or without `esModuleInterop`, when `skipLibCheck` is off.
  - **Test:** a test checks that `ref` receives the API.

  ## Compatibility

  - Compared with alpha.10, the published types differ only in `RefObject` → `Ref` and `JSX.Element` → `ReactElement`.
  - I checked a small consumer (no ref, a `useRef` ref, a `RefObject<GoslingRef>` ref, a callback ref) against `@types/react` 16.9, 17, 18.3 and 19.1 with `skipLibCheck` off. All compile.
  - Runtime behaviour is unchanged. `GoslingComponent` reads `ref` from props, so **`ref` only works on React 19**. On React ≤18 it stays `null`, the same as in alpha.10. A `forwardRef` wrapper would
  fix that but changes what kind of export `GoslingComponent` is, so it's left for a later PR.

  ## Testing

  - `tsc -p tsconfig.build.json` passes.
  - `vitest`: 150 tests pass.
  - Type errors in the full project match `v2` exactly; all of them predate this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a8758486bb7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.