# Issue

**Title:** Bump rollup from 2.79.1 to 2.79.2

## Description

Bumps [rollup](https://github.com/rollup/rollup) from 2.79.1 to 2.79.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rollup/rollup/blob/master/CHANGELOG.md">rollup's changelog</a>.</em></p>
<blockquote>
<h1>rollup changelog</h1>
<h2>4.22.5</h2>
<p><em>2024-09-27</em></p>
<h3>Bug Fixes</h3>
<ul>
<li>Allow parsing of certain unicode characters again (<a href="">#5674</a>)</li>
</ul>
<h3>Pull Requests</h3>
<ul>
<li><a href="">#5674</a>: Fix panic with unicode characters (<a href="https://github.com/sapphi-red"><code>@​sapphi-red</code></a>, <a href="https://github.com/lukastaegert"><code>@​lukastaegert</code></a>)</li>
<li><a href="">#5675</a>: chore(deps): update dependency rollup to v4.22.4 [security] (<a href="https://github.com/renovate"><code>@​renovate</code></a>[bot])</li>
<li><a href="">#5680</a>: chore(deps): update dependency <code>@​rollup/plugin-commonjs</code> to v28 (<a href="https://github.com/renovate"><code>@​renovate</code></a>[bot], <a href="https://github.com/lukastaegert"><code>@​lukastaegert</code></a>)</li>
<li><a href="">#5681</a>: chore(deps): update dependency <code>@​rollup/plugin-replace</code> to v6 (<a href="https://github.com/renovate"><code>@​renovate</code></a>[bot])</li>
<li><a href="">#5682</a>: chore(deps): update dependency <code>@​rollup/plugin-typescript</code> to v12 (<a href="https://github.com/renovate"><code>@​renovate</code></a>[bot])</li>
<li><a href="">#5684</a>: chore(deps): lock file maintenance minor/patch updates (<a href="https://github.com/renovate"><code>@​renovate</code></a>[bot])</li>
</ul>
<h2>4.22.4</h2>
<p><em>2024-09-21</em></p>
<h3>Bug Fixes</h3>
<ul>
<li>Fix a vulnerability in generated code that affects IIFE, UMD and CJS bundles when run in a browser context (<a href="">#5671</a>)</li>
</ul>
<h3>Pull Requests</h3>
<ul>
<li><a href="">#5670</a>: refactor: Use object.prototype to check for reserved properties (<a href="https://github.com/YuHyeonWook"><code>@​YuHyeonWook</code></a>)</li>
<li><a href="">#5671</a>: Fix DOM Clobbering CVE (<a href="https://github.com/lukastaegert"><code>@​lukastaegert</code></a>)</li>
</ul>
<h2>4.22.3</h2>
<p><em>2024-09-21</em></p>
<h3>Bug Fixes</h3>
<ul>
<li>Ensure that mutations in modules without side effects are observed while properly handling transitive dependencies (<a href="">#5669</a>)</li>
</ul>
<h3>Pull Requests</h3>
<ul>
<li><a href="">#5669</a>: Ensure impure dependencies of pure modules are added (<a href="https://github.com/lukastaegert"><code>@​lukastaegert</code></a>)</li>
</ul>
<h2>4.22.2</h2>
<p><em>2024-09-20</em></p>
<h3>Bug Fixes</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c9bd03d</code></a> 2.79.2</li>
<li><a href=""><code>48aef33</code></a> fix: resolve DOM Clobbering CVE-2024-43788 (backport to v2) (<a href="">#5677</a>)</li>
<li>See full diff in <a href="https://github.com/rollup/rollup/compare/v2.79.1...v2.79.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rollup&package-manager=npm_and_yarn&previous-version=2.79.1&new-version=2.79.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/biowasm/aioli/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5279a9732f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.