# Issue

**Title:** Bump webpack-cli from 7.2.3 to 7.3.1

## Description

Bumps [webpack-cli](https://github.com/webpack/webpack-cli) from 7.2.3 to 7.3.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/webpack/webpack-cli/releases">webpack-cli's releases</a>.</em></p>
<blockquote>
<h2>webpack-cli@7.3.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p>fix: detect missing package managers and failed installations, without a lock file the CLI chose npm even when it wasn't installed instead of yarn or pnpm, and it continued after a package failed to install (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4889</a>)</p>
</li>
<li>
<p>chore: replace the <code>import-local</code> and <code>cross-spawn</code> dependencies with Node.js built-ins (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4889</a>)</p>
</li>
<li>
<p>chore: load configuration files with <code>import()</code> instead of <code>eval</code> (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4893</a>)</p>
</li>
</ul>
<h2>webpack-cli@7.3.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p>feat: run <code>webpack-dev-server@6</code> as a compiler plugin. The CLI drives watch compilation, prints build stats and closes the compiler on shutdown. Older dev servers continue to manage their own compilation. (by <a href="https://github.com/bjohansebas"><code>@​bjohansebas</code></a> in <a href="">#4847</a>)</p>
<p>In multi-compiler mode, every dev server serves all compilers by default. Use the new <code>--dev-server-per-compiler</code> option of <code>webpack serve</code> to serve each compiler only by the dev server from its own configuration.</p>
</li>
<li>
<p>feat: add shell completions for zsh, bash, fish and powershell through the <code>complete</code> command (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4840</a>)</p>
</li>
</ul>
<h3>Patch Changes</h3>
<ul>
<li>
<p>fix: keep multi-compiler options such as <code>parallelism</code> and <code>plugins</code> set on a configuration array when <code>--config-name</code> or <code>extends</code> rebuild it (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4871</a>)</p>
</li>
<li>
<p>perf: share the compile cache with child processes and worker threads, such as minimizer workers, so they start warm too (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4872</a>)</p>
</li>
<li>
<p>fix: assign distinct ports to dev servers of configurations that share the same <code>devServer</code> object. (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4886</a>)</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/webpack/webpack-cli/blob/main/CHANGELOG.md">webpack-cli's changelog</a>.</em></p>
<blockquote>
<h2>7.3.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p>fix: detect missing package managers and failed installations, without a lock file the CLI chose npm even when it wasn't installed instead of yarn or pnpm, and it continued after a package failed to install (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4889</a>)</p>
</li>
<li>
<p>chore: replace the <code>import-local</code> and <code>cross-spawn</code> dependencies with Node.js built-ins (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4889</a>)</p>
</li>
<li>
<p>chore: load configuration files with <code>import()</code> instead of <code>eval</code> (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4893</a>)</p>
</li>
</ul>
<h2>7.3.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>
<p>feat: run <code>webpack-dev-server@6</code> as a compiler plugin. The CLI drives watch compilation, prints build stats and closes the compiler on shutdown. Older dev servers continue to manage their own compilation. (by <a href="https://github.com/bjohansebas"><code>@​bjohansebas</code></a> in <a href="">#4847</a>)</p>
<p>In multi-compiler mode, every dev server serves all compilers by default. Use the new <code>--dev-server-per-compiler</code> option of <code>webpack serve</code> to serve each compiler only by the dev server from its own configuration.</p>
</li>
<li>
<p>feat: add shell completions for zsh, bash, fish and powershell through the <code>complete</code> command (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4840</a>)</p>
</li>
</ul>
<h3>Patch Changes</h3>
<ul>
<li>
<p>fix: keep multi-compiler options such as <code>parallelism</code> and <code>plugins</code> set on a configuration array when <code>--config-name</code> or <code>extends</code> rebuild it (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4871</a>)</p>
</li>
<li>
<p>perf: share the compile cache with child processes and worker threads, such as minimizer workers, so they start warm too (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4872</a>)</p>
</li>
<li>
<p>fix: assign distinct ports to dev servers of configurations that share the same <code>devServer</code> object. (by <a href="https://github.com/alexander-akait"><code>@​alexander-akait</code></a> in <a href="">#4886</a>)</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3a695da</code></a> chore(release): new release (<a href="">#4891</a>)</li>
<li><a href=""><code>4a88999</code></a> chore: load configuration files without eval (<a href="">#4893</a>)</li>
<li><a href=""><code>02a85ac</code></a> chore(deps): bump the dependencies group across 1 directory with 5 updates (#...</li>
<li><a href=""><code>3942417</code></a> chore: replace import-local and cross-spawn with Node.js built-ins (<a href="">#4889</a>)</li>
<li><a href=""><code>349b660</code></a> chore(release): new release (<a href="">#4841</a>)</li>
<li><a href=""><code>d4ee8bd</code></a> fix: assign distinct ports to dev servers sharing devServer options (<a href="">#4886</a>)</li>
<li><a href=""><code>9bcb6d5</code></a> feat: run webpack-dev-server as a compiler plugin (<a href="">#4847</a>)</li>
<li><a href=""><code>b32b0c9</code></a> test: make the generator and dev server tests stable (<a href="">#4885</a>)</li>
<li><a href=""><code>351f1c9</code></a> chore(deps): bump the dependencies group across 1 directory with 9 updates (#...</li>
<li><a href=""><code>701e74b</code></a> chore(deps-dev): bump del-cli from 7.0.0 to 8.0.1 (<a href="">#4880</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/webpack/webpack-cli/compare/webpack-cli@7.2.3...webpack-cli@7.3.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=webpack-cli&package-manager=npm_and_yarn&previous-version=7.2.3&new-version=7.3.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c87d2045aacf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.