# Issue

**Title:** Bump pytest from 8.3.5 to 9.0.2

## Description

Bumps [pytest](https://github.com/pytest-dev/pytest) from 8.3.5 to 9.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pytest-dev/pytest/releases">pytest's releases</a>.</em></p>
<blockquote>
<h2>9.0.2</h2>
<h1>pytest 9.0.2 (2025-12-06)</h1>
<h2>Bug fixes</h2>
<ul>
<li>
<p><a href="">#13896</a>: The terminal progress feature added in pytest 9.0.0 has been disabled by default, except on Windows, due to compatibility issues with some terminal emulators.</p>
<p>You may enable it again by passing <code>-p terminalprogress</code>. We may enable it by default again once compatibility improves in the future.</p>
<p>Additionally, when the environment variable <code>TERM</code> is <code>dumb</code>, the escape codes are no longer emitted, even if the plugin is enabled.</p>
</li>
<li>
<p><a href="">#13904</a>: Fixed the TOML type of the <code>tmp_path_retention_count</code> settings in the API reference from number to string.</p>
</li>
<li>
<p><a href="">#13946</a>: The private <code>config.inicfg</code> attribute was changed in a breaking manner in pytest 9.0.0.
Due to its usage in the ecosystem, it is now restored to working order using a compatibility shim.
It will be deprecated in pytest 9.1 and removed in pytest 10.</p>
</li>
<li>
<p><a href="">#13965</a>: Fixed quadratic-time behavior when handling <code>unittest</code> subtests in Python 3.10.</p>
</li>
</ul>
<h2>Improved documentation</h2>
<ul>
<li><a href="">#4492</a>: The API Reference now contains cross-reference-able documentation of <code>pytest's command-line flags &lt;command-line-flags&gt;</code>.</li>
</ul>
<h2>9.0.1</h2>
<h1>pytest 9.0.1 (2025-11-12)</h1>
<h2>Bug fixes</h2>
<ul>
<li><a href="">#13895</a>: Restore support for skipping tests via <code>raise unittest.SkipTest</code>.</li>
<li><a href="">#13896</a>: The terminal progress plugin added in pytest 9.0 is now automatically disabled when iTerm2 is detected, it generated desktop notifications instead of the desired functionality.</li>
<li><a href="">#13904</a>: Fixed the TOML type of the verbosity settings in the API reference from number to string.</li>
<li><a href="">#13910</a>: Fixed <!-- raw HTML omitted -->UserWarning: Do not expect file_or_dir<!-- raw HTML omitted --> on some earlier Python 3.12 and 3.13 point versions.</li>
</ul>
<h2>Packaging updates and notes for downstreams</h2>
<ul>
<li><a href="">#13933</a>: The tox configuration has been adjusted to make sure the desired
version string can be passed into its <code>package_env</code> through
the <code>SETUPTOOLS_SCM_PRETEND_VERSION_FOR_PYTEST</code> environment
variable as a part of the release process -- by <code>webknjaz</code>.</li>
</ul>
<h2>Contributor-facing changes</h2>
<ul>
<li><a href="">#13891</a>, <a href="">#13942</a>: The CI/CD part of the release automation is now capable of
creating GitHub Releases without having a Git checkout on
disk -- by <code>bluetech</code> and <code>webknjaz</code>.</li>
<li><a href="">#13933</a>: The tox configuration has been adjusted to make sure the desired
version string can be passed into its <code>package_env</code> through
the <code>SETUPTOOLS_SCM_PRETEND_VERSION_FOR_PYTEST</code> environment
variable as a part of the release process -- by <code>webknjaz</code>.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3d10b51</code></a> Prepare release version 9.0.2</li>
<li><a href=""><code>188750b</code></a> Merge pull request <a href="">#14030</a> from pytest-dev/patchback/backports/9.0.x/1e4b01d1f...</li>
<li><a href=""><code>b7d7bef</code></a> Merge pull request <a href="">#14014</a> from bluetech/compat-note</li>
<li><a href=""><code>bd08e85</code></a> Merge pull request <a href="">#14013</a> from pytest-dev/patchback/backports/9.0.x/922b60377...</li>
<li><a href=""><code>bc78386</code></a> Add CLI options reference documentation (<a href="">#13930</a>)</li>
<li><a href=""><code>5a4e398</code></a> Fix docs typo (<a href="">#14005</a>) (<a href="">#14008</a>)</li>
<li><a href=""><code>d7ae6df</code></a> Merge pull request <a href="">#14006</a> from pytest-dev/maintenance/update-plugin-list-tmpl...</li>
<li><a href=""><code>556f6a2</code></a> pre-commit: fix rst-lint after new release (<a href="">#13999</a>) (<a href="">#14001</a>)</li>
<li><a href=""><code>c60fbe6</code></a> Fix quadratic-time behavior when handling <code>unittest</code> subtests in Python 3.10 ...</li>
<li><a href=""><code>73d9b01</code></a> Merge pull request <a href="">#13995</a> from nicoddemus/patchback/backports/9.0.x/1b5200c0f...</li>
<li>Additional commits viewable in <a href="https://github.com/pytest-dev/pytest/compare/8.3.5...9.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pytest&package-manager=pip&previous-version=8.3.5&new-version=9.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

You can trigger a rebase of this PR by commenting `@dependabot rebase`.

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

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ad23cde9c0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.