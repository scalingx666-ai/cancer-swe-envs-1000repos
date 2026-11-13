# Issue

**Title:** Bump nx and @nx/vite in /democlient

## Description

Bumps [nx](https://github.com/nrwl/nx/tree/HEAD/packages/nx) and [@nx/vite](https://github.com/nrwl/nx/tree/HEAD/packages/vite). These dependencies needed to be updated together.
Updates `nx` from 22.0.2 to 22.7.12
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nrwl/nx/releases">nx's releases</a>.</em></p>
<blockquote>
<h2>22.7.12 (2026-09-10)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> box JsonFileSet payload to keep HashInstruction small (<a href="">#36247</a>, <a href="">#35248</a>, <a href="">#36244</a>, <a href="">#36152</a>)</li>
<li><strong>core:</strong> replace per-input visited clones with undo-log scoping in hash planner (<a href="">#36248</a>, <a href="">#35071</a>, <a href="">#36152</a>, <a href="">#34971</a>, <a href="">#36244</a>, <a href="">#35248</a>, <a href="">#36247</a>)</li>
<li><strong>core:</strong> intern hash instructions in a pool and plan with id lists (<a href="">#36249</a>, <a href="">#35071</a>, <a href="">#36152</a>, <a href="">#36248</a>, <a href="">#36244</a>)</li>
<li><strong>core:</strong> fall back to v8 for oversized daemon responses and length-prefix the wire protocol (<a href="">#36838</a>, <a href="">#36850</a>, <a href="">#36794</a>, <a href="">#36754</a>)</li>
<li><strong>core:</strong> remove redundant <code>allWorkspaceFiles</code> from the project graph pipeline (<a href="">#34425</a>)</li>
<li><strong>core:</strong> share workspace fileset hash results instead of deep-cloning per task (<a href="">#36244</a>, <a href="">#34971</a>, <a href="">#34942</a>)</li>
<li><strong>core:</strong> reduce task hashing memory usage on large workspaces (<a href="">#36267</a>, <a href="">#36152</a>, <a href="">#36249</a>)</li>
<li><strong>core:</strong> avoid mutating target options when resolving configurations (<a href="">#36934</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Craigory Coppola <a href="https://github.com/AgentEnder"><code>@​AgentEnder</code></a></li>
<li>FrozenPandaz <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
<li>Jason Jean <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
<li>Leosvel Pérez Espinosa <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
<li>Nicolas Beaussart <a href="https://github.com/beaussan"><code>@​beaussan</code></a></li>
</ul>
<h2>22.7.11 (2026-09-09)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> release per-run process listeners and task history results (<a href="">#36974</a>, <a href="">#36866</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Craigory Coppola <a href="https://github.com/AgentEnder"><code>@​AgentEnder</code></a></li>
<li>FrozenPandaz <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
</ul>
<h2>22.7.10 (2026-09-09)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> validate the migrations path before extracting package migrations (<a href="">#36887</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Jason Jean <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
<li>Leosvel Pérez Espinosa <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
</ul>
<h2>22.7.9 (2026-09-01)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> restrict daemon and plugin worker socket access to the owning user (<a href="">#36370</a>, <a href="">#36586</a>, <a href="">#36463</a>)</li>
<li><strong>core:</strong> compare daemon workspace roots case-insensitively on Windows (<a href="">#36835</a>, <a href="">#36722</a>)</li>
<li><strong>core:</strong> close daemon log descriptors after spawn to avoid Node 26 crash (<a href="">#36280</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7c5b4dc</code></a> docs(core): correct the NX_MAX_MESSAGE_SIZE row and drop a stale clause</li>
<li><a href=""><code>3163430</code></a> chore(core): format daemon client with prettier</li>
<li><a href=""><code>ab613f7</code></a> chore(core): satisfy cargo fmt on the backported hash planner</li>
<li><a href=""><code>1cffd59</code></a> fix(core): avoid mutating target options when resolving configurations (<a href="">#36934</a>)</li>
<li><a href=""><code>8d81ae2</code></a> fix(core): reduce task hashing memory usage on large workspaces (<a href="">#36267</a>)</li>
<li><a href=""><code>bfd3e51</code></a> fix(core): share workspace fileset hash results instead of deep-cloning per t...</li>
<li><a href=""><code>02f82fa</code></a> cleanup(core): persist file-set hash caches on the TaskHasher instance (<a href="">#36118</a>)</li>
<li><a href=""><code>2c34a3b</code></a> fix(core): remove redundant <code>allWorkspaceFiles</code> from the project graph pipeli...</li>
<li><a href=""><code>73a415b</code></a> fix(core): fall back to v8 for oversized daemon responses and length-prefix t...</li>
<li><a href=""><code>a25009d</code></a> fix(core): intern hash instructions in a pool and plan with id lists (<a href="">#36249</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/nrwl/nx/commits/22.7.12/packages/nx">compare view</a></li>
</ul>
</details>
<details>
<summary>Install script changes</summary>
<p>This version modifies <code>postinstall</code> script that runs during installation. Review the package contents before updating.</p>
</details>
<br />

Updates `@nx/vite` from 22.0.2 to 22.7.12
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nrwl/nx/releases">@​nx/vite's releases</a>.</em></p>
<blockquote>
<h2>22.7.12 (2026-09-10)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> box JsonFileSet payload to keep HashInstruction small (<a href="">#36247</a>, <a href="">#35248</a>, <a href="">#36244</a>, <a href="">#36152</a>)</li>
<li><strong>core:</strong> replace per-input visited clones with undo-log scoping in hash planner (<a href="">#36248</a>, <a href="">#35071</a>, <a href="">#36152</a>, <a href="">#34971</a>, <a href="">#36244</a>, <a href="">#35248</a>, <a href="">#36247</a>)</li>
<li><strong>core:</strong> intern hash instructions in a pool and plan with id lists (<a href="">#36249</a>, <a href="">#35071</a>, <a href="">#36152</a>, <a href="">#36248</a>, <a href="">#36244</a>)</li>
<li><strong>core:</strong> fall back to v8 for oversized daemon responses and length-prefix the wire protocol (<a href="">#36838</a>, <a href="">#36850</a>, <a href="">#36794</a>, <a href="">#36754</a>)</li>
<li><strong>core:</strong> remove redundant <code>allWorkspaceFiles</code> from the project graph pipeline (<a href="">#34425</a>)</li>
<li><strong>core:</strong> share workspace fileset hash results instead of deep-cloning per task (<a href="">#36244</a>, <a href="">#34971</a>, <a href="">#34942</a>)</li>
<li><strong>core:</strong> reduce task hashing memory usage on large workspaces (<a href="">#36267</a>, <a href="">#36152</a>, <a href="">#36249</a>)</li>
<li><strong>core:</strong> avoid mutating target options when resolving configurations (<a href="">#36934</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Craigory Coppola <a href="https://github.com/AgentEnder"><code>@​AgentEnder</code></a></li>
<li>FrozenPandaz <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
<li>Jason Jean <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
<li>Leosvel Pérez Espinosa <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
<li>Nicolas Beaussart <a href="https://github.com/beaussan"><code>@​beaussan</code></a></li>
</ul>
<h2>22.7.11 (2026-09-09)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> release per-run process listeners and task history results (<a href="">#36974</a>, <a href="">#36866</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Craigory Coppola <a href="https://github.com/AgentEnder"><code>@​AgentEnder</code></a></li>
<li>FrozenPandaz <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
</ul>
<h2>22.7.10 (2026-09-09)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> validate the migrations path before extracting package migrations (<a href="">#36887</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Jason Jean <a href="https://github.com/FrozenPandaz"><code>@​FrozenPandaz</code></a></li>
<li>Leosvel Pérez Espinosa <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
</ul>
<h2>22.7.9 (2026-09-01)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>core:</strong> restrict daemon and plugin worker socket access to the owning user (<a href="">#36370</a>, <a href="">#36586</a>, <a href="">#36463</a>)</li>
<li><strong>core:</strong> compare daemon workspace roots case-insensitively on Windows (<a href="">#36835</a>, <a href="">#36722</a>)</li>
<li><strong>core:</strong> close daemon log descriptors after spawn to avoid Node 26 crash (<a href="">#36280</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d84f424</code></a> fix(devkit): expand <code>@​nx/devkit/</code>internal re-exports for cherry-picked v23 deep...</li>
<li><a href=""><code>ac81879</code></a> fix(repo): revert deep-import rewrites that targeted v23-only <code>@​nx/devkit/</code>inte...</li>
<li><a href=""><code>7e4bce9</code></a> feat(testing): add migration for Jest 30 snapshot guide link (<a href="">#35629</a>)</li>
<li><a href=""><code>cdca177</code></a> chore(repo): declare lazy-loaded packages as implicit deps (<a href="">#35392</a>)</li>
<li><a href=""><code>b02e138</code></a> fix(misc): resolve pnpm catalog: refs in version lookups (<a href="">#35459</a>)</li>
<li><a href=""><code>6c6d399</code></a> feat(vite): add compiler option to vite plugin for tsgo support (<a href="">#35429</a>)</li>
<li><a href=""><code>4bbd4b1</code></a> chore(repo): migrate nx repo to eslint v9 flat config (<a href="">#35359</a>)</li>
<li><a href=""><code>1507788</code></a> chore(repo): short-circuit isUsingTsSolutionSetup in unit tests (<a href="">#35371</a>)</li>
<li><a href=""><code>878ec01</code></a> fix(vitest): infer ancestor tsconfig files as test task inputs (<a href="">#35241</a>)</li>
<li><a href=""><code>931f86c</code></a> fix(vitest): add dependent task output files as inputs for vitest test target...</li>
<li>Additional commits viewable in <a href="https://github.com/nrwl/nx/commits/22.7.12/packages/vite">compare view</a></li>
</ul>
</details>
<br />

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/Azure-Samples/healthcare-agent-orchestrator/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e9f2f7a5718`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.