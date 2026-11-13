# Issue

**Title:** Bump @vitest/mocker and vitest in /democlient

## Description

Bumps [@vitest/mocker](https://github.com/vitest-dev/vitest/tree/HEAD/packages/mocker) and [vitest](https://github.com/vitest-dev/vitest/tree/HEAD/packages/vitest). These dependencies needed to be updated together.
Updates `@vitest/mocker` from 3.2.4 to 4.1.12
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitest-dev/vitest/releases">@​vitest/mocker's releases</a>.</em></p>
<blockquote>
<h2>v4.1.12</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>mocker</strong>: Harden manual and redirect mocks [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11580</a> <a href=""><!-- raw HTML omitted -->(b8253)<!-- raw HTML omitted --></a></li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.11...v4.1.12">View changes on GitHub</a></h5>
<h2>v4.1.11</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li>Revive global concurrency limit for test lifecycle [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> and <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a> in <a href="">vitest-dev/vitest#10992</a> <a href=""><!-- raw HTML omitted -->(5146d)<!-- raw HTML omitted --></a></li>
<li><strong>browser</strong>:
<ul>
<li>Encode iframeId in tester iframe URL [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a>, <strong>Pduhard</strong> and <strong>Claude Opus 4.8</strong> in <a href="">vitest-dev/vitest#10955</a> <a href=""><!-- raw HTML omitted -->(10b2c)<!-- raw HTML omitted --></a></li>
<li>Trigger playwright/chromium gc on lower disk availability [backport to v4]  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>OpenCode</strong> in <a href="">vitest-dev/vitest#10951</a> <a href=""><!-- raw HTML omitted -->(9851d)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>mocker</strong>:
<ul>
<li>Restrict redirect mocks to the fs allowlist [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#10974</a> <a href=""><!-- raw HTML omitted -->(fe5a1)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.10...v4.1.11">View changes on GitHub</a></h5>
<h2>v4.1.10</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>browser</strong>: Check fs access in builtin commands [backport to v4]  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>OpenCode (claude-opus-4-8)</strong> in <a href="">vitest-dev/vitest#10680</a> <a href=""><!-- raw HTML omitted -->(5c18d)<!-- raw HTML omitted --></a></li>
<li><strong>vm</strong>: Fix external module resolve error with deps optimizer query for encoded URI [backport to v4]  -  by <a href="https://github.com/SveLil"><code>@​SveLil</code></a> and <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a> in <a href="">vitest-dev/vitest#10661</a> <a href=""><!-- raw HTML omitted -->(bae52)<!-- raw HTML omitted --></a></li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.9...v4.1.10">View changes on GitHub</a></h5>
<h2>v4.1.9</h2>
<h3>🐞 Bug Fixes</h3>
<ul>
<li>Fix <code>importOriginal</code> with optimizer and query import [backport to v4] - by <strong>Hiroshi Ogawa</strong>, <strong>David Harris</strong>, <strong>Codex</strong>and <strong>Vladimir</strong> in <a href="">vitest-dev/vitest#10546</a> <a href=""><!-- raw HTML omitted -->(a5180)<!-- raw HTML omitted --></a></li>
<li><strong>browser</strong>:
<ul>
<li>Wait for orchestrator readiness before resolving browser sessions [backport to v4] - by <strong>Vladimir</strong> and <strong>Séamus O'Connor</strong> in <a href="">vitest-dev/vitest#10555</a> <a href=""><!-- raw HTML omitted -->(7fb29)<!-- raw HTML omitted --></a></li>
<li>Wait for iframe tester readiness before preparing  [backport to v4] - by <strong>Vladimir</strong> and <strong>Séamus O'Connor</strong> in <a href="">vitest-dev/vitest#10497</a> and <a href="">vitest-dev/vitest#10556</a> <a href=""><!-- raw HTML omitted -->(fbc62)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>mocker</strong>:
<ul>
<li>Hoist vi.mock() for vite-plus/test imports [backport to v4] - by <strong>Hiroshi Ogawa</strong>, <strong>LongYinan</strong>, <strong>Claude Opus 4.8</strong> and <strong>Vladimir</strong> in <a href="">vitest-dev/vitest#10548</a> <a href=""><!-- raw HTML omitted -->(2c955)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>pool</strong>:
<ul>
<li>Prevent test run hang on worker crash  [backport to v4] - by <strong>Ari Perkkiö</strong> and <strong>Jattioui Ismail</strong> in <a href="">vitest-dev/vitest#10543</a> and <a href="">vitest-dev/vitest#10564</a> <a href=""><!-- raw HTML omitted -->(934b0)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5><a href="https://github.com/vitest-dev/vitest/compare/v4.1.8...v4.1.9">View changes on GitHub</a></h5>
<h2>v4.1.8</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>browser</strong>:
<ul>
<li>Disable client <code>cdp</code> API when <code>allowWrite/allowExec: false</code> [backport to v4]  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a> and <strong>Codex</strong> in <a href="">vitest-dev/vitest#10450</a> <a href=""><!-- raw HTML omitted -->(e4067)<!-- raw HTML omitted --></a></li>
<li>Remove orphaned Playwright route when same module is mocked via multiple ids [backport to v4]  -  by <a href="https://github.com/toxik"><code>@​toxik</code></a> and <a href="https://github.com/Zelys-DFKH"><code>@​Zelys-DFKH</code></a> in <a href="">vitest-dev/vitest#10474</a> <a href=""><!-- raw HTML omitted -->(675b4)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.7...v4.1.8">View changes on GitHub</a></h5>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4766ce1</code></a> chore: release v4.1.12 (<a href="">#11610</a>)</li>
<li><a href=""><code>b825313</code></a> fix(mocker): harden manual and redirect mocks [backport to v4] (<a href="">#11580</a>)</li>
<li><a href=""><code>9bd8d46</code></a> chore: release v4.1.11 (<a href="">#10995</a>)</li>
<li><a href=""><code>fe5a11d</code></a> fix(mocker): restrict redirect mocks to the fs allowlist [backport to v4] (<a href="">#1</a>...</li>
<li><a href=""><code>db616d2</code></a> chore: release v4.1.10 (<a href="">#10718</a>)</li>
<li><a href=""><code>a7a61e7</code></a> chore: release v4.1.9 (<a href="">#10598</a>)</li>
<li><a href=""><code>2c9559c</code></a> fix(mocker): hoist vi.mock() for vite-plus/test imports [backport to v4] (<a href="">#10</a>...</li>
<li><a href=""><code>e61f2dd</code></a> chore: release v4.1.8</li>
<li><a href=""><code>a09d472</code></a> chore: release v4.1.7</li>
<li><a href=""><code>a8fd24c</code></a> chore: release v4.1.6</li>
<li>Additional commits viewable in <a href="https://github.com/vitest-dev/vitest/commits/v4.1.12/packages/mocker">compare view</a></li>
</ul>
</details>
<details>
<summary>Maintainer changes</summary>
<p>This version was pushed to npm by <a href="https://www.npmjs.com/~GitHub%20Actions">GitHub Actions</a>, a new releaser for <code>@​vitest/mocker</code> since your current version.</p>
</details>
<br />

Updates `vitest` from 3.2.4 to 4.1.12
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitest-dev/vitest/releases">vitest's releases</a>.</em></p>
<blockquote>
<h2>v4.1.12</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>mocker</strong>: Harden manual and redirect mocks [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11580</a> <a href=""><!-- raw HTML omitted -->(b8253)<!-- raw HTML omitted --></a></li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.11...v4.1.12">View changes on GitHub</a></h5>
<h2>v4.1.11</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li>Revive global concurrency limit for test lifecycle [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> and <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a> in <a href="">vitest-dev/vitest#10992</a> <a href=""><!-- raw HTML omitted -->(5146d)<!-- raw HTML omitted --></a></li>
<li><strong>browser</strong>:
<ul>
<li>Encode iframeId in tester iframe URL [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a>, <strong>Pduhard</strong> and <strong>Claude Opus 4.8</strong> in <a href="">vitest-dev/vitest#10955</a> <a href=""><!-- raw HTML omitted -->(10b2c)<!-- raw HTML omitted --></a></li>
<li>Trigger playwright/chromium gc on lower disk availability [backport to v4]  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>OpenCode</strong> in <a href="">vitest-dev/vitest#10951</a> <a href=""><!-- raw HTML omitted -->(9851d)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>mocker</strong>:
<ul>
<li>Restrict redirect mocks to the fs allowlist [backport to v4]  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#10974</a> <a href=""><!-- raw HTML omitted -->(fe5a1)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.10...v4.1.11">View changes on GitHub</a></h5>
<h2>v4.1.10</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>browser</strong>: Check fs access in builtin commands [backport to v4]  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>OpenCode (claude-opus-4-8)</strong> in <a href="">vitest-dev/vitest#10680</a> <a href=""><!-- raw HTML omitted -->(5c18d)<!-- raw HTML omitted --></a></li>
<li><strong>vm</strong>: Fix external module resolve error with deps optimizer query for encoded URI [backport to v4]  -  by <a href="https://github.com/SveLil"><code>@​SveLil</code></a> and <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a> in <a href="">vitest-dev/vitest#10661</a> <a href=""><!-- raw HTML omitted -->(bae52)<!-- raw HTML omitted --></a></li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.9...v4.1.10">View changes on GitHub</a></h5>
<h2>v4.1.9</h2>
<h3>🐞 Bug Fixes</h3>
<ul>
<li>Fix <code>importOriginal</code> with optimizer and query import [backport to v4] - by <strong>Hiroshi Ogawa</strong>, <strong>David Harris</strong>, <strong>Codex</strong>and <strong>Vladimir</strong> in <a href="">vitest-dev/vitest#10546</a> <a href=""><!-- raw HTML omitted -->(a5180)<!-- raw HTML omitted --></a></li>
<li><strong>browser</strong>:
<ul>
<li>Wait for orchestrator readiness before resolving browser sessions [backport to v4] - by <strong>Vladimir</strong> and <strong>Séamus O'Connor</strong> in <a href="">vitest-dev/vitest#10555</a> <a href=""><!-- raw HTML omitted -->(7fb29)<!-- raw HTML omitted --></a></li>
<li>Wait for iframe tester readiness before preparing  [backport to v4] - by <strong>Vladimir</strong> and <strong>Séamus O'Connor</strong> in <a href="">vitest-dev/vitest#10497</a> and <a href="">vitest-dev/vitest#10556</a> <a href=""><!-- raw HTML omitted -->(fbc62)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>mocker</strong>:
<ul>
<li>Hoist vi.mock() for vite-plus/test imports [backport to v4] - by <strong>Hiroshi Ogawa</strong>, <strong>LongYinan</strong>, <strong>Claude Opus 4.8</strong> and <strong>Vladimir</strong> in <a href="">vitest-dev/vitest#10548</a> <a href=""><!-- raw HTML omitted -->(2c955)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>pool</strong>:
<ul>
<li>Prevent test run hang on worker crash  [backport to v4] - by <strong>Ari Perkkiö</strong> and <strong>Jattioui Ismail</strong> in <a href="">vitest-dev/vitest#10543</a> and <a href="">vitest-dev/vitest#10564</a> <a href=""><!-- raw HTML omitted -->(934b0)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5><a href="https://github.com/vitest-dev/vitest/compare/v4.1.8...v4.1.9">View changes on GitHub</a></h5>
<h2>v4.1.8</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>browser</strong>:
<ul>
<li>Disable client <code>cdp</code> API when <code>allowWrite/allowExec: false</code> [backport to v4]  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a> and <strong>Codex</strong> in <a href="">vitest-dev/vitest#10450</a> <a href=""><!-- raw HTML omitted -->(e4067)<!-- raw HTML omitted --></a></li>
<li>Remove orphaned Playwright route when same module is mocked via multiple ids [backport to v4]  -  by <a href="https://github.com/toxik"><code>@​toxik</code></a> and <a href="https://github.com/Zelys-DFKH"><code>@​Zelys-DFKH</code></a> in <a href="">vitest-dev/vitest#10474</a> <a href=""><!-- raw HTML omitted -->(675b4)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v4.1.7...v4.1.8">View changes on GitHub</a></h5>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4766ce1</code></a> chore: release v4.1.12 (<a href="">#11610</a>)</li>
<li><a href=""><code>5bf2197</code></a> chore: delete wdio folder from v4 branch to avoid falsy release (<a href="">#11581</a>)</li>
<li><a href=""><code>9bd8d46</code></a> chore: release v4.1.11 (<a href="">#10995</a>)</li>
<li><a href=""><code>9851dbc</code></a> fix(browser): trigger playwright/chromium gc on lower disk availability [back...</li>
<li><a href=""><code>db616d2</code></a> chore: release v4.1.10 (<a href="">#10718</a>)</li>
<li><a href=""><code>bae52b5</code></a> fix(vm): fix external module resolve error with deps optimizer query for enco...</li>
<li><a href=""><code>a7a61e7</code></a> chore: release v4.1.9 (<a href="">#10598</a>)</li>
<li><a href=""><code>934b0f5</code></a> fix(pool): prevent test run hang on worker crash (<a href="">#10543</a>) [backport to v4] (#...</li>
<li><a href=""><code>7fb2965</code></a> fix(browser): wait for orchestrator readiness before resolving browser sessio...</li>
<li><a href=""><code>a518019</code></a> fix: fix <code>importOriginal</code> with optimizer and query import [backport to v4] (#...</li>
<li>Additional commits viewable in <a href="https://github.com/vitest-dev/vitest/commits/v4.1.12/packages/vitest">compare view</a></li>
</ul>
</details>
<details>
<summary>Maintainer changes</summary>
<p>This version was pushed to npm by <a href="https://www.npmjs.com/~GitHub%20Actions">GitHub Actions</a>, a new releaser for vitest since your current version.</p>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1c78153b9f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.