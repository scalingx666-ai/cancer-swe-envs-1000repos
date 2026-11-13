# Issue

**Title:** Bump the actions group with 3 updates

## Description

Bumps the actions group with 3 updates: [docker/login-action](https://github.com/docker/login-action), [github/codeql-action](https://github.com/github/codeql-action) and [zizmorcore/zizmor-action](https://github.com/zizmorcore/zizmor-action).

Updates `docker/login-action` from 4.7.0 to 4.8.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.8.0</h2>
<ul>
<li>Set Docker Hub OIDC token lifetime default to 1 hour by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1070</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> and <code>@​aws-sdk/client-ecr-public</code> to 3.1161.0 in <a href="">docker/login-action#1103</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.107.0 to 0.109.0 in <a href="">docker/login-action#1105</a></li>
<li>Bump vite from 7.3.6 to 7.3.7 in <a href="">docker/login-action#1101</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.7.0...v4.8.0">https://github.com/docker/login-action/compare/v4.7.0...v4.8.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8aa5831</code></a> Merge pull request <a href="">#1105</a> from docker/dependabot/npm_and_yarn/docker/actions-t...</li>
<li><a href=""><code>043f81d</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>3ff6998</code></a> build(deps): bump <code>@​docker/actions-toolkit</code> from 0.107.0 to 0.109.0</li>
<li><a href=""><code>694ef6a</code></a> Merge pull request <a href="">#1103</a> from docker/dependabot/npm_and_yarn/aws-sdk-dependen...</li>
<li><a href=""><code>7c6e412</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>aa2441f</code></a> build(deps): bump the aws-sdk-dependencies group across 1 directory with 2 up...</li>
<li><a href=""><code>d6c10b0</code></a> Merge pull request <a href="">#1106</a> from docker/dependabot/github_actions/codeql-actions...</li>
<li><a href=""><code>319f1ee</code></a> Merge pull request <a href="">#1104</a> from docker/dependabot/github_actions/actions/setup-...</li>
<li><a href=""><code>b483b7f</code></a> Merge pull request <a href="">#1101</a> from docker/dependabot/npm_and_yarn/vite-7.3.7</li>
<li><a href=""><code>dc7d67c</code></a> Merge pull request <a href="">#1070</a> from crazy-max/increase-oidc-default-expiry</li>
<li>Additional commits viewable in <a href="https://github.com/docker/login-action/compare/v4.7.0...v4.8.0">compare view</a></li>
</ul>
</details>
<br />

Updates `github/codeql-action` from 4.39.1 to 4.39.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/github/codeql-action/releases">github/codeql-action's releases</a>.</em></p>
<blockquote>
<h2>v4.39.3</h2>
<ul>
<li>Fixed diff-informed alert filtering incorrectly removing alerts in changed files whose paths contain spaces, special characters, or non-ASCII characters. <a href="">#4283</a></li>
</ul>
<h2>v4.39.2</h2>
<ul>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.27.4">2.27.4</a>. <a href="">#4284</a></li>
<li><em>Upcoming breaking change</em>: CodeQL version 2.22.3 and earlier were discontinued on 16 October 2026 alongside GitHub Enterprise Server 3.18, and will be unsupported by the next minor release of the CodeQL Action. Added a deprecation warning for customers using these versions of CodeQL. <a href="">#4266</a></li>
<li>Starting with macOS 27 and Xcode 27, traced analyses are unsupported. See <a href="https://github.blog/changelog/2026-10-19-codeql-changes-for-macos-27-xcode-27-and-swift-6-4/">this blog post for more information</a>. The CodeQL Action will now try to identify if a workflow is about to perform a traced analysis on version 27 or above of macOS or Xcode. If so, the CodeQL Action will emit a corresponding warning that will also be visible on the <a href="https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/manage-your-configuration/use-the-tools-status-page-for-code-scanning">Tool Status Page</a>. This check will be rolled out following this release of the CodeQL Action. <a href="">#4221</a></li>
<li>The undocumented TRAP cache cleanup feature that could be enabled using the <code>CODEQL_ACTION_CLEANUP_TRAP_CACHES</code> environment variable has been removed, as announced in the release notes for CodeQL Action 4.35.2. The <code>analyze</code> Action now warns if this environment variable is set. If you used TRAP cache cleanup to limit Actions cache usage, we recommend disabling TRAP caching by passing the <code>trap-caching: false</code> input to the <code>init</code> Action. <a href="">#4243</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/github/codeql-action/blob/main/CHANGELOG.md">github/codeql-action's changelog</a>.</em></p>
<blockquote>
<h2>4.39.3 - 04 Nov 2026</h2>
<ul>
<li>Fixed diff-informed alert filtering incorrectly removing alerts in changed files whose paths contain spaces, special characters, or non-ASCII characters. <a href="">#4283</a></li>
</ul>
<h2>4.39.2 - 03 Nov 2026</h2>
<ul>
<li>Update default CodeQL bundle version to <a href="https://github.com/github/codeql-action/releases/tag/codeql-bundle-v2.27.4">2.27.4</a>. <a href="">#4284</a></li>
<li><em>Upcoming breaking change</em>: CodeQL version 2.22.3 and earlier were discontinued on 16 October 2026 alongside GitHub Enterprise Server 3.18, and will be unsupported by the next minor release of the CodeQL Action. Added a deprecation warning for customers using these versions of CodeQL. <a href="">#4266</a></li>
<li>Starting with macOS 27 and Xcode 27, traced analyses are unsupported. See <a href="https://github.blog/changelog/2026-10-19-codeql-changes-for-macos-27-xcode-27-and-swift-6-4/">this blog post for more information</a>. The CodeQL Action will now try to identify if a workflow is about to perform a traced analysis on version 27 or above of macOS or Xcode. If so, the CodeQL Action will emit a corresponding warning that will also be visible on the <a href="https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/manage-your-configuration/use-the-tools-status-page-for-code-scanning">Tool Status Page</a>. This check will be rolled out following this release of the CodeQL Action. <a href="">#4221</a></li>
<li>The undocumented TRAP cache cleanup feature that could be enabled using the <code>CODEQL_ACTION_CLEANUP_TRAP_CACHES</code> environment variable has been removed, as announced in the release notes for CodeQL Action 4.35.2. The <code>analyze</code> Action now warns if this environment variable is set. If you used TRAP cache cleanup to limit Actions cache usage, we recommend disabling TRAP caching by passing the <code>trap-caching: false</code> input to the <code>init</code> Action. <a href="">#4243</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>33d7b85</code></a> Merge pull request <a href="">#4299</a> from github/update-v4.39.3-064910ba2</li>
<li><a href=""><code>24393f8</code></a> Update changelog for v4.39.3</li>
<li><a href=""><code>064910b</code></a> Merge pull request <a href="">#4297</a> from github/mbg/update-glob</li>
<li><a href=""><code>f532ac5</code></a> Update <code>glob</code> to <code>14.0.3</code></li>
<li><a href=""><code>8cd4dfa</code></a> Merge pull request <a href="">#4280</a> from github/mbg/ci/validate-yaml</li>
<li><a href=""><code>cea289b</code></a> Return different exit code when a language is not recognised</li>
<li><a href=""><code>7287bb3</code></a> Remove <code>exclude</code> entry that's no longer needed</li>
<li><a href=""><code>8eb7cdf</code></a> Use normal <code>.editorconfig</code> pattern</li>
<li><a href=""><code>160e547</code></a> Merge remote-tracking branch 'origin/main' into mbg/ci/validate-yaml</li>
<li><a href=""><code>913e1bb</code></a> Merge pull request <a href="">#4283</a> from github/sam-robson/decode-diff-informed-sarif-uris</li>
<li>Additional commits viewable in <a href="https://github.com/github/codeql-action/compare/v4.39.1...v4.39.3">compare view</a></li>
</ul>
</details>
<br />

Updates `zizmorcore/zizmor-action` from 0.8.0 to 0.8.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/zizmorcore/zizmor-action/releases">zizmorcore/zizmor-action's releases</a>.</em></p>
<blockquote>
<h2>v0.8.1</h2>
<p><a href="https://github.com/sponsors/woodruffw/">Sponsorship is appreciated!</a></p>
<p>zizmor 1.32 is now the default version used by this action.</p>
<p>Full release notes: <a href="https://docs.zizmor.sh/release-notes/%5B#1320%5D()">zizmorcore/zizmor-action#1320</a></p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/zizmorcore/zizmor-action/compare/v0.8.0...v0.8.1">https://github.com/zizmorcore/zizmor-action/compare/v0.8.0...v0.8.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>45d7276</code></a> Sync zizmor versions (<a href="">#191</a>)</li>
<li><a href=""><code>ff38741</code></a> chore(deps): bump the github-actions group across 1 directory with 2 updates ...</li>
<li><a href=""><code>4a9eca4</code></a> README: another troubleshooting section (<a href="">#186</a>)</li>
<li><a href=""><code>83a0416</code></a> Bump pins (<a href="">#185</a>)</li>
<li>See full diff in <a href="https://github.com/zizmorcore/zizmor-action/compare/53290badfa369cb0bf7ad16342cb62c2fa47ac7b...45d7276c9ca790aabd705e31ca99c6185c3e76dd">compare view</a></li>
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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9489852b1f64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.