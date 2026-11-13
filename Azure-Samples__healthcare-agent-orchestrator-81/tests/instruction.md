# Issue

**Title:** Bump follow-redirects, @nx/vite and nx in /democlient

## Description

Removes [follow-redirects](https://github.com/follow-redirects/follow-redirects). It's no longer used after updating ancestor dependencies [follow-redirects](https://github.com/follow-redirects/follow-redirects), [@nx/vite](https://github.com/nrwl/nx/tree/HEAD/packages/vite) and [nx](https://github.com/nrwl/nx/tree/HEAD/packages/nx). These dependencies need to be updated together.

Removes `follow-redirects`

Updates `@nx/vite` from 22.7.12 to 24.0.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nrwl/nx/releases">@​nx/vite's releases</a>.</em></p>
<blockquote>
<h2>24.0.2 (2026-10-26)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>angular:</strong> register the ssr dev server afterEmit hook only once (<a href="">#37589</a>, <a href="">#37587</a>)</li>
<li><strong>angular-rspack:</strong> refresh SSR apps after server changes (<a href="">#37607</a>, <a href="">#37586</a>)</li>
<li><strong>core:</strong> allow options in object dependsOn entries of project and nx.json schemas (<a href="">#37600</a>)</li>
<li><strong>core:</strong> fail run-commands tasks that exit before printing readyWhen text (<a href="">#37591</a>)</li>
<li><strong>core:</strong> honor run-commands readyWhen for a single command in a terminal (<a href="">#37594</a>)</li>
<li><strong>core:</strong> preserve completed task timings across TUI modes (<a href="">#37592</a>)</li>
<li><strong>core:</strong> exit 1 on --nx-bail and show why batch tasks were skipped (<a href="">#37604</a>)</li>
<li><strong>core:</strong> await file watcher registration before reporting readiness (<a href="">#37076</a>)</li>
<li><strong>nextjs:</strong> bump Next.js 15 and 16 to releases patching critical RCEs (<a href="">#37601</a>)</li>
<li><strong>testing:</strong> select the test files jest runs for atomized targets (<a href="">#37505</a>)</li>
<li><strong>testing:</strong> infer the serve task from bunx-prefixed playwright webServer commands (<a href="">#37606</a>, <a href="">#37597</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Craigory Coppola <a href="https://github.com/AgentEnder"><code>@​AgentEnder</code></a></li>
<li>Leosvel Pérez Espinosa <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
<li>leosvelperez <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
<li>MaxKless <a href="https://github.com/MaxKless"><code>@​MaxKless</code></a></li>
<li>sarankumar <a href="https://github.com/sarankumar1325"><code>@​sarankumar1325</code></a></li>
</ul>
<h2>24.0.1 (2026-10-23)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>angular-rspack:</strong> install the plugin after Angular dependencies (<a href="">#37562</a>)</li>
<li><strong>core:</strong> resolve pnpm aliased dependencies to their own snapshot (<a href="">#37538</a>, <a href="">#37429</a>)</li>
<li><strong>core:</strong> drop repository-local git env from the ai-config clone (<a href="">#37498</a>, <a href="">#37436</a>)</li>
<li><strong>core:</strong> pin the package manager version in generated workspaces (<a href="">#37261</a>)</li>
<li><strong>core:</strong> match project patterns with unknown colon prefixes or regex characters (<a href="">#37500</a>)</li>
<li><strong>core:</strong> keep migrations.json and prompt files out of migrate commits (<a href="">#37530</a>)</li>
<li><strong>core:</strong> load Nx Cloud code in the daemon with Node's native .js loader (<a href="">#37534</a>)</li>
<li><strong>core:</strong> keep the daemon running when PROCESS_IN_BACKGROUND fails (<a href="">#37535</a>)</li>
<li><strong>core:</strong> stop readyWhen logMatches from matching Nx command lines (<a href="">#37550</a>)</li>
<li><strong>core:</strong> avoid MaxListenersExceededWarning on Nx Cloud agents (<a href="">#37553</a>)</li>
<li><strong>core:</strong> let readyWhen read the NX_READY_URL its producer reports (<a href="">#37554</a>)</li>
<li><strong>core:</strong> name every pending dependency in the readiness wait line (<a href="">#37555</a>)</li>
<li><strong>core:</strong> avoid MaxListenersExceededWarning with parallel run-commands (<a href="">#37556</a>)</li>
<li><strong>core:</strong> preserve TUI task start times across mode switches (<a href="">#37558</a>)</li>
<li><strong>core:</strong> recover external dependencies after configuration errors (<a href="">#37560</a>)</li>
<li><strong>core:</strong> avoid pnpm store probes during version detection (<a href="">#37561</a>)</li>
<li><strong>core:</strong> count every run-commands readyWhen match, including on stderr (<a href="">#37567</a>)</li>
<li><strong>core:</strong> exit 1, not 130, when dependents of a failed task are skipped (<a href="">#37574</a>, <a href="">#37506</a>)</li>
<li><strong>maven:</strong> suppress wire payloads in verbose batch builds (<a href="">#37566</a>)</li>
<li><strong>misc:</strong> write versioned docs lockfile into the staging dir (<a href="">#37546</a>)</li>
<li><strong>nx-plugin:</strong> preserve the working directory in generated e2e tests (<a href="">#37565</a>)</li>
<li><strong>release:</strong> stop release e2e flaking on the GitHub username lookup (<a href="">#37544</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>e7ffd79</code></a> feat(core): wait for dev servers by default, with a 10-minute readiness timeo...</li>
<li><a href=""><code>65e71bb</code></a> feat(node): report readiness from generated server apps with emitReadySignal ...</li>
<li><a href=""><code>dc5dac1</code></a> fix(misc): harden v24 migrations (<a href="">#37493</a>)</li>
<li><a href=""><code>2541ec6</code></a> feat(misc): add dev server readiness to the remaining plugins (<a href="">#37483</a>)</li>
<li><a href=""><code>b6d2631</code></a> feat(core): let dev servers signal readiness instead of guessing their port (...</li>
<li><a href=""><code>a34dff2</code></a> fix(misc): stop generators from accepting targets on removed executors (<a href="">#37475</a>)</li>
<li><a href=""><code>b58ec0d</code></a> fix(js): framework plugins defer typecheck to <code>@​nx/js/</code>typescript (<a href="">#37342</a>)</li>
<li><a href=""><code>b798ad0</code></a> feat(misc): remove deprecated executors (<a href="">#37160</a>)</li>
<li><a href=""><code>a53a55f</code></a> feat(misc): migrate removed config helpers with loadable stubs (<a href="">#37156</a>)</li>
<li><a href=""><code>8443a64</code></a> feat(core): give nx migrate --run-migration the same agent flow as full runs ...</li>
<li>Additional commits viewable in <a href="https://github.com/nrwl/nx/commits/24.0.2/packages/vite">compare view</a></li>
</ul>
</details>
<br />

Updates `nx` from 22.7.12 to 24.0.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nrwl/nx/releases">nx's releases</a>.</em></p>
<blockquote>
<h2>24.0.2 (2026-10-26)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>angular:</strong> register the ssr dev server afterEmit hook only once (<a href="">#37589</a>, <a href="">#37587</a>)</li>
<li><strong>angular-rspack:</strong> refresh SSR apps after server changes (<a href="">#37607</a>, <a href="">#37586</a>)</li>
<li><strong>core:</strong> allow options in object dependsOn entries of project and nx.json schemas (<a href="">#37600</a>)</li>
<li><strong>core:</strong> fail run-commands tasks that exit before printing readyWhen text (<a href="">#37591</a>)</li>
<li><strong>core:</strong> honor run-commands readyWhen for a single command in a terminal (<a href="">#37594</a>)</li>
<li><strong>core:</strong> preserve completed task timings across TUI modes (<a href="">#37592</a>)</li>
<li><strong>core:</strong> exit 1 on --nx-bail and show why batch tasks were skipped (<a href="">#37604</a>)</li>
<li><strong>core:</strong> await file watcher registration before reporting readiness (<a href="">#37076</a>)</li>
<li><strong>nextjs:</strong> bump Next.js 15 and 16 to releases patching critical RCEs (<a href="">#37601</a>)</li>
<li><strong>testing:</strong> select the test files jest runs for atomized targets (<a href="">#37505</a>)</li>
<li><strong>testing:</strong> infer the serve task from bunx-prefixed playwright webServer commands (<a href="">#37606</a>, <a href="">#37597</a>)</li>
</ul>
<h3>❤️ Thank You</h3>
<ul>
<li>Craigory Coppola <a href="https://github.com/AgentEnder"><code>@​AgentEnder</code></a></li>
<li>Leosvel Pérez Espinosa <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
<li>leosvelperez <a href="https://github.com/leosvelperez"><code>@​leosvelperez</code></a></li>
<li>MaxKless <a href="https://github.com/MaxKless"><code>@​MaxKless</code></a></li>
<li>sarankumar <a href="https://github.com/sarankumar1325"><code>@​sarankumar1325</code></a></li>
</ul>
<h2>24.0.1 (2026-10-23)</h2>
<h3>🩹 Fixes</h3>
<ul>
<li><strong>angular-rspack:</strong> install the plugin after Angular dependencies (<a href="">#37562</a>)</li>
<li><strong>core:</strong> resolve pnpm aliased dependencies to their own snapshot (<a href="">#37538</a>, <a href="">#37429</a>)</li>
<li><strong>core:</strong> drop repository-local git env from the ai-config clone (<a href="">#37498</a>, <a href="">#37436</a>)</li>
<li><strong>core:</strong> pin the package manager version in generated workspaces (<a href="">#37261</a>)</li>
<li><strong>core:</strong> match project patterns with unknown colon prefixes or regex characters (<a href="">#37500</a>)</li>
<li><strong>core:</strong> keep migrations.json and prompt files out of migrate commits (<a href="">#37530</a>)</li>
<li><strong>core:</strong> load Nx Cloud code in the daemon with Node's native .js loader (<a href="">#37534</a>)</li>
<li><strong>core:</strong> keep the daemon running when PROCESS_IN_BACKGROUND fails (<a href="">#37535</a>)</li>
<li><strong>core:</strong> stop readyWhen logMatches from matching Nx command lines (<a href="">#37550</a>)</li>
<li><strong>core:</strong> avoid MaxListenersExceededWarning on Nx Cloud agents (<a href="">#37553</a>)</li>
<li><strong>core:</strong> let readyWhen read the NX_READY_URL its producer reports (<a href="">#37554</a>)</li>
<li><strong>core:</strong> name every pending dependency in the readiness wait line (<a href="">#37555</a>)</li>
<li><strong>core:</strong> avoid MaxListenersExceededWarning with parallel run-commands (<a href="">#37556</a>)</li>
<li><strong>core:</strong> preserve TUI task start times across mode switches (<a href="">#37558</a>)</li>
<li><strong>core:</strong> recover external dependencies after configuration errors (<a href="">#37560</a>)</li>
<li><strong>core:</strong> avoid pnpm store probes during version detection (<a href="">#37561</a>)</li>
<li><strong>core:</strong> count every run-commands readyWhen match, including on stderr (<a href="">#37567</a>)</li>
<li><strong>core:</strong> exit 1, not 130, when dependents of a failed task are skipped (<a href="">#37574</a>, <a href="">#37506</a>)</li>
<li><strong>maven:</strong> suppress wire payloads in verbose batch builds (<a href="">#37566</a>)</li>
<li><strong>misc:</strong> write versioned docs lockfile into the staging dir (<a href="">#37546</a>)</li>
<li><strong>nx-plugin:</strong> preserve the working directory in generated e2e tests (<a href="">#37565</a>)</li>
<li><strong>release:</strong> stop release e2e flaking on the GitHub username lookup (<a href="">#37544</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a93cf7c</code></a> fix(core): await file watcher registration before reporting readiness (<a href="">#37076</a>)</li>
<li><a href=""><code>a5de223</code></a> fix(core): exit 1 on --nx-bail and show why batch tasks were skipped (<a href="">#37604</a>)</li>
<li><a href=""><code>5c36e0e</code></a> fix(core): preserve completed task timings across TUI modes (<a href="">#37592</a>)</li>
<li><a href=""><code>e4cdb6b</code></a> fix(core): honor run-commands readyWhen for a single command in a terminal (#...</li>
<li><a href=""><code>c8814f6</code></a> fix(core): fail run-commands tasks that exit before printing readyWhen text (...</li>
<li><a href=""><code>dcacb43</code></a> fix(core): allow options in object dependsOn entries of project and nx.json s...</li>
<li><a href=""><code>70e7c33</code></a> fix(core): exit 1, not 130, when dependents of a failed task are skipped (<a href="">#37</a>...</li>
<li><a href=""><code>d88fd0b</code></a> fix(core): count every run-commands readyWhen match, including on stderr (<a href="">#37</a>...</li>
<li><a href=""><code>3149837</code></a> fix(core): avoid pnpm store probes during version detection (<a href="">#37561</a>)</li>
<li><a href=""><code>20ae7b0</code></a> fix(core): recover external dependencies after configuration errors (<a href="">#37560</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/nrwl/nx/commits/24.0.2/packages/nx">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c17de436adf3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.