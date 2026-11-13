# Issue

**Title:** fix(jbrowse-web): React's dev render-logging read the destroyed SessionLoader

## Description

`reloadPluginManagerCallback` is a plugin-facing entry point. Destroying the `SessionLoader` when the app detaches it made every later read of that loader a use-after-free, and React reads it again in the same passive-effect flush.

### The read that lands on the corpse

React 19's dev-mode `logComponentRender` runs in `commitPassiveMountOnFiber` — the passive **mount** phase, which follows the passive **unmount** phase in the same flush. It diffs each component's props via `addObjectDiffToProperties`, which recurses into the props object and reads every property. `Renderer`'s props hold the `loader`.

So the order within one flush is: the lifecycle effect's cleanup destroys the superseded loader, and then, a few frames later on the same stack, React reads every property off it:

```
Object.get [as configPath]
addObjectDiffToProperties (react-dom-client.development.js:3967)
addObjectDiffToProperties (react-dom-client.development.js:4015)
logComponentRender          (react-dom-client.development.js:4129)
commitPassiveMountOnFiber   (react-dom-client.development.js:15468)
```

For a scalar prop that is a liveliness warning per attribute. For an **array**-typed prop it is a hard throw: the child node's observable instance is still `UNINITIALIZED`, so the read calls `createObservableInstance`, which asserts `state === NodeLifeCycle.INITIALIZING` — and a dead node fails it:

```
Uncaught Error: [mobx-state-tree] assertion failed: the creation of the
observable instance must be done on the initializing phase
```

Reported from Apollo, whose login flow reloads: storing the OAuth token calls `setRole()`, which flips the `role` volatile and re-fires the session autorun that issues the reload.

### Reproduction

Driving the real reload against a **development** build in Chrome gives 18 `SessionLoader` liveliness warnings, one per attribute — matching the report. With this branch, 0.

This is dev-only and browser-only, which is why it had no coverage: `logComponentRender` does not run in a production build, and does not run under jsdom, so neither the jest suites nor a `pnpm build` browser test can see it.

### The fix

**The loader is no longer destroyed on detach.** `deactivate()` already releases the build autorun and the rootModel, and React drops the state reference on the swap, so it was ordinary garbage. Freeing it bought nothing and cost every subsequent reader — React's own, and any plugin's.

**The reload callback declines when the loader is already superseded.** A plugin can legitimately issue the callback more than once off one rootModel; Apollo's per-internet-account loop does, with no `break`, from an async autorun whose synchronous prefix can re-fire and leave several continuations in flight. The second call previously ran `reloadSessionLoader()` over the dead node — `getSnapshot()` and `setSuperseded()` on a destroyed `SessionLoader` — and, since liveliness only warns, went on to swap in a third loader built from the corpse, discarding the replacement the first call had correctly produced.

### Test

`repeatReload.test.tsx` mounts the real lifecycle, reaches `reloadPluginManagerCallback` the way a plugin does, calls it, detaches, and calls it again. On `main` the second call builds a second replacement and emits `SessionLoader` liveliness warnings; the test asserts one replacement and no warnings. It covers the repeat-call half — the `logComponentRender` half is not reachable from jsdom, and the browser probe for it is not included here.

`disposeLoader.test.ts`'s superseded case is updated to the new contract: the loader has to survive detach for a late caller to read it and decline.

### Note

The branch carries a separate `chore(docs)` commit regenerating the model tables, stale on `main` since 2eeaf1023d. Unrelated to the fix.

`scripts/check-docs.ts` also fails on `main` (`packages/app-core/CLAUDE.md:220` references `DockviewRightHeaderActions`, a component ADR-068 deliberately deleted — the prose is correct and the checker is over-eager). Left alone rather than papered over here.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf90911fe2d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.