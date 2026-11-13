# Issue

**Title:** chore(deps-dev): bump ruff from 0.17.1 to 0.17.2 in the minor-and-patch group

## Description

Bumps the minor-and-patch group with 1 update: [ruff](https://github.com/astral-sh/ruff).

Updates `ruff` from 0.17.1 to 0.17.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/releases">ruff's releases</a>.</em></p>
<blockquote>
<h2>0.17.2</h2>
<h2>Release Notes</h2>
<p>Released on 2026-10-22.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>complexity</code>] Add <code>unnecessary-regular-expression-compile</code> (<a href="">#25533</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>Avoid syntax errors for type variables with starred constraints (<code>UP040</code>, <code>UP046</code>, <code>UP047</code>, <code>RUF053</code>) (<a href="">#28362</a>)</li>
<li>[<code>pydocstyle</code>] Treat backslash-escaped <code>*args</code> and <code>**kwargs</code> as documented (<code>D417</code>) (<a href="">#29536</a>)</li>
<li>[<code>pylint</code>] Avoid false positive on starred elements (<code>PLE0643</code>) (<a href="">#29483</a>)</li>
<li>[<code>pylint</code>] Mark fixes unsafe when deleting comments (<code>PLR5501</code>, <code>PLW0120</code>) (<a href="">#29414</a>)</li>
<li>[<code>pyupgrade</code>] Mark fix unsafe when deleting comments (<code>UP035</code>) (<a href="">#29413</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid intermediate names in lint name resolution (<a href="">#29506</a>)</li>
<li>Prefilter bidirectional Unicode checks by UTF-8 leading bytes (<a href="">#29561</a>)</li>
<li>Share postfix parsing and reduce expression copies (<a href="">#29480</a>)</li>
</ul>
<h3>Configuration</h3>
<ul>
<li>[<code>pylint</code>] Add a configurable allowlist for <code>magic-value-comparison</code> (<code>PLR2004</code>) (<a href="">#18961</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Clarify documentation and correct stale guidance (<a href="">#29374</a>)</li>
<li>[<code>pyupgrade</code>] Remove mentions of variance related to fix safety (<code>UP040</code>, <code>UP047</code>) (<a href="">#29592</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/fixfon"><code>@​fixfon</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/FrancescoPezzella"><code>@​FrancescoPezzella</code></a></li>
<li><a href="https://github.com/anishgirianish"><code>@​anishgirianish</code></a></li>
<li><a href="https://github.com/rajveer3x"><code>@​rajveer3x</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/LckyLke"><code>@​LckyLike</code></a></li>
<li><a href="https://github.com/DaniBodor"><code>@​DaniBodor</code></a></li>
</ul>
<h2>Install ruff 0.17.2</h2>
<h3>Install prebuilt binaries via shell script</h3>
<pre lang="sh"><code>curl --proto '=https' --tlsv1.2 -LsSf https://releases.astral.sh/github/ruff/releases/download/0.17.2/ruff-installer.sh | sh
&lt;/tr&gt;&lt;/table&gt;
</code></pre>
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/blob/main/CHANGELOG.md">ruff's changelog</a>.</em></p>
<blockquote>
<h2>0.17.2</h2>
<p>Released on 2026-10-22.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>complexity</code>] Add <code>unnecessary-regular-expression-compile</code> (<a href="">#25533</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>Avoid syntax errors for type variables with starred constraints (<code>UP040</code>, <code>UP046</code>, <code>UP047</code>, <code>RUF053</code>) (<a href="">#28362</a>)</li>
<li>[<code>pydocstyle</code>] Treat backslash-escaped <code>*args</code> and <code>**kwargs</code> as documented (<code>D417</code>) (<a href="">#29536</a>)</li>
<li>[<code>pylint</code>] Avoid false positive on starred elements (<code>PLE0643</code>) (<a href="">#29483</a>)</li>
<li>[<code>pylint</code>] Mark fixes unsafe when deleting comments (<code>PLR5501</code>, <code>PLW0120</code>) (<a href="">#29414</a>)</li>
<li>[<code>pyupgrade</code>] Mark fix unsafe when deleting comments (<code>UP035</code>) (<a href="">#29413</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid intermediate names in lint name resolution (<a href="">#29506</a>)</li>
<li>Prefilter bidirectional Unicode checks by UTF-8 leading bytes (<a href="">#29561</a>)</li>
<li>Share postfix parsing and reduce expression copies (<a href="">#29480</a>)</li>
</ul>
<h3>Configuration</h3>
<ul>
<li>[<code>pylint</code>] Add a configurable allowlist for <code>magic-value-comparison</code> (<code>PLR2004</code>) (<a href="">#18961</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Clarify documentation and correct stale guidance (<a href="">#29374</a>)</li>
<li>[<code>pyupgrade</code>] Remove mentions of variance related to fix safety (<code>UP040</code>, <code>UP047</code>) (<a href="">#29592</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/fixfon"><code>@​fixfon</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/FrancescoPezzella"><code>@​FrancescoPezzella</code></a></li>
<li><a href="https://github.com/anishgirianish"><code>@​anishgirianish</code></a></li>
<li><a href="https://github.com/rajveer3x"><code>@​rajveer3x</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/LckyLke"><code>@​LckyLike</code></a></li>
<li><a href="https://github.com/DaniBodor"><code>@​DaniBodor</code></a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>30516b4</code></a> Bump version to 0.17.2 (<a href="">#29637</a>)</li>
<li><a href=""><code>59a9e85</code></a> [ty] Generalize nested types in inferred return types (<a href="">#29488</a>)</li>
<li><a href=""><code>0d562aa</code></a> [ty] Check inherited attribute conflicts (<a href="">#28559</a>)</li>
<li><a href=""><code>48dcdd0</code></a> [ty] Restrict range implications from gradual equivalence (<a href="">#29577</a>)</li>
<li><a href=""><code>734d75a</code></a> [ty] Check for unsatisfiable bodies before existentially quantifying (<a href="">#29504</a>)</li>
<li><a href=""><code>b0f9526</code></a> [ty] Preserve checks for recursive descriptor setter types (<a href="">#29148</a>)</li>
<li><a href=""><code>32869b4</code></a> Avoid creating deployments for automation jobs (<a href="">#29626</a>)</li>
<li><a href=""><code>ec891ba</code></a> Link the commit in pull request report footers (<a href="">#29621</a>)</li>
<li><a href=""><code>8958748</code></a> [ty] Publish ecosystem reports from GitHub Actions (<a href="">#29609</a>)</li>
<li><a href=""><code>01f5394</code></a> [ty] Publish typing conformance reports from GitHub Actions (<a href="">#29608</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ruff/compare/0.17.1...0.17.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=ruff&package-manager=uv&previous-version=0.17.1&new-version=0.17.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8261893d9b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.