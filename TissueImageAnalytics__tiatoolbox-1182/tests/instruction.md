# Issue

**Title:** ⬆️ Bump the openlayers-version-updates group in /tiatoolbox/visualization/openlayers with 6 updates

## Description

Bumps the openlayers-version-updates group in /tiatoolbox/visualization/openlayers with 6 updates:

| Package | From | To |
| --- | --- | --- |
| [@vitest/coverage-v8](https://github.com/vitest-dev/vitest/tree/HEAD/packages/coverage-v8) | `5.0.3` | `5.0.5` |
| [@vitest/eslint-plugin](https://github.com/vitest-dev/eslint-plugin-vitest) | `1.6.27` | `1.6.28` |
| [eslint](https://github.com/eslint/eslint) | `10.12.0` | `10.13.0` |
| [jsdom](https://github.com/jsdom/jsdom) | `30.1.2` | `30.1.3` |
| [vite](https://github.com/vitejs/vite/tree/HEAD/packages/vite) | `8.3.4` | `8.3.5` |
| [vitest](https://github.com/vitest-dev/vitest/tree/HEAD/packages/vitest) | `5.0.3` | `5.0.5` |

Updates `@vitest/coverage-v8` from 5.0.3 to 5.0.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitest-dev/vitest/releases">@​vitest/coverage-v8's releases</a>.</em></p>
<blockquote>
<h2>v5.0.5</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li>Keep vite default <code>fs.deny</code> with api token file  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11578</a> <a href=""><!-- raw HTML omitted -->(28dc1)<!-- raw HTML omitted --></a></li>
<li>Handle quoted file names in <code>--changed</code>  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11583</a> <a href=""><!-- raw HTML omitted -->(14921)<!-- raw HTML omitted --></a></li>
<li>Add <code>data</code> to the <code>import.meta.hot</code> stub  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11590</a> <a href=""><!-- raw HTML omitted -->(3a828)<!-- raw HTML omitted --></a></li>
<li>Set <code>skip</code> in <code>skipIf</code>, ignore <code>undefined</code> options  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11591</a> <a href=""><!-- raw HTML omitted -->(d523a)<!-- raw HTML omitted --></a></li>
<li>Skip builtin loading in async leak detector  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11598</a> <a href=""><!-- raw HTML omitted -->(fe86a)<!-- raw HTML omitted --></a></li>
<li>Keep the import frame in native loader errors  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11599</a> <a href=""><!-- raw HTML omitted -->(9697b)<!-- raw HTML omitted --></a></li>
<li>Run hook cleanups when a later hook fails  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11605</a> <a href=""><!-- raw HTML omitted -->(6c5a4)<!-- raw HTML omitted --></a></li>
<li>Release mocks of finished test files  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11607</a> <a href=""><!-- raw HTML omitted -->(e9c3d)<!-- raw HTML omitted --></a></li>
<li>Abort all running tests on cancel  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11606</a> <a href=""><!-- raw HTML omitted -->(6621a)<!-- raw HTML omitted --></a></li>
<li><strong>browser</strong>:
<ul>
<li>Ignore synthetic pagehide events  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11582</a> <a href=""><!-- raw HTML omitted -->(ca081)<!-- raw HTML omitted --></a></li>
<li>Run plugin buildStart on server creation  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11593</a> <a href=""><!-- raw HTML omitted -->(ea611)<!-- raw HTML omitted --></a></li>
<li>Drop late connections of closed sessions  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11600</a> <a href=""><!-- raw HTML omitted -->(f161e)<!-- raw HTML omitted --></a></li>
<li>Wait 30s for the browser to close  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11601</a> <a href=""><!-- raw HTML omitted -->(6498b)<!-- raw HTML omitted --></a></li>
<li>Run global setup once with instances  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11596</a> <a href=""><!-- raw HTML omitted -->(8dd67)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>reporter</strong>:
<ul>
<li>End reason <code>&amp;;failed&amp;;</code> on worker crash  -  by <a href="https://github.com/AriPerkkio"><code>@​AriPerkkio</code></a> in <a href="">vitest-dev/vitest#11568</a> <a href=""><!-- raw HTML omitted -->(6ae8e)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v5.0.4...v5.0.5">View changes on GitHub</a></h5>
<h2>v5.0.4</h2>
<h3>   🚀 Features</h3>
<ul>
<li><strong>experimental</strong>:
<ul>
<li>Tag cache directories with CACHEDIR.TAG  -  by <a href="https://github.com/lifeiscontent"><code>@​lifeiscontent</code></a> in <a href="">vitest-dev/vitest#11461</a> <a href=""><!-- raw HTML omitted -->(a8ea3)<!-- raw HTML omitted --></a></li>
<li>Support <code>test.ui.theme</code> option  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11499</a> <a href=""><!-- raw HTML omitted -->(1da66)<!-- raw HTML omitted --></a></li>
<li>Highlight selector multiple matches in trace view  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11489</a> <a href=""><!-- raw HTML omitted -->(5abba)<!-- raw HTML omitted --></a></li>
<li>Print how many tests were affected and a total when running <code>--changed</code>  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11424</a> <a href=""><!-- raw HTML omitted -->(a2336)<!-- raw HTML omitted --></a></li>
<li>Add an option to cache dependencies instead of statically parsing them  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11515</a> <a href=""><!-- raw HTML omitted -->(c0601)<!-- raw HTML omitted --></a></li>
<li>Add fit and zoom controls to trace viewer  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11490</a> <a href=""><!-- raw HTML omitted -->(f5dd9)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li>Fail the run on git and location filter errors  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11430</a> <a href=""><!-- raw HTML omitted -->(30d03)<!-- raw HTML omitted --></a></li>
<li>Enable fsModuleCache by default  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11435</a> <a href=""><!-- raw HTML omitted -->(ad208)<!-- raw HTML omitted --></a></li>
<li>Track project files and mocks with --changed  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11432</a> <a href=""><!-- raw HTML omitted -->(b0f2b)<!-- raw HTML omitted --></a></li>
<li>Refactor caching, fix <code>:</code> in project and change the shape of <code>results</code> cache  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11453</a> <a href=""><!-- raw HTML omitted -->(9673c)<!-- raw HTML omitted --></a></li>
<li>Keep full <code>$</code> string values when <code>taskTitleValueFormatTruncate</code> is 0  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11485</a> <a href=""><!-- raw HTML omitted -->(4f7e1)<!-- raw HTML omitted --></a></li>
<li>Resolve node builtins in client environments  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11417</a> <a href=""><!-- raw HTML omitted -->(56b31)<!-- raw HTML omitted --></a></li>
<li>Fix module graph builtin externals after <a href="">#11421</a>  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11491</a> and <a href="">vitest-dev/vitest#11421</a> <a href=""><!-- raw HTML omitted -->(008e1)<!-- raw HTML omitted --></a></li>
<li>Wrap module mocks during in-source testing  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11505</a> <a href=""><!-- raw HTML omitted -->(36d19)<!-- raw HTML omitted --></a></li>
<li>Handle line endings in snapshot  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11522</a> <a href=""><!-- raw HTML omitted -->(4c468)<!-- raw HTML omitted --></a></li>
<li>Respect root in projects  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11521</a> <a href=""><!-- raw HTML omitted -->(26642)<!-- raw HTML omitted --></a></li>
<li>Resolve mocks in directories with spaces  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11539</a> <a href=""><!-- raw HTML omitted -->(caaef)<!-- raw HTML omitted --></a></li>
<li><strong>api</strong>:
<ul>
<li>Publish the api token atomically  -  by <a href="https://github.com/umairnawaz333"><code>@​umairnawaz333</code></a> in <a href="">vitest-dev/vitest#11323</a> <a href=""><!-- raw HTML omitted -->(6f990)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>browser</strong>:</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7a825db</code></a> chore: release v5.0.5 (<a href="">#11609</a>)</li>
<li><a href=""><code>6a11cf6</code></a> chore: release v5.0.4 (<a href="">#11554</a>)</li>
<li><a href=""><code>2297d93</code></a> fix(coverage): v8 browser memory leak between test files (<a href="">#11466</a>)</li>
<li><a href=""><code>c74e099</code></a> fix(deps): update all non-major dependencies (<a href="">#11167</a>)</li>
<li>See full diff in <a href="https://github.com/vitest-dev/vitest/commits/v5.0.5/packages/coverage-v8">compare view</a></li>
</ul>
</details>
<br />

Updates `@vitest/eslint-plugin` from 1.6.27 to 1.6.28
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitest-dev/eslint-plugin-vitest/releases">@​vitest/eslint-plugin's releases</a>.</em></p>
<blockquote>
<h2>v1.6.28</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li><strong>parse-vitest-fn-call</strong>: Recognize member-form hooks like <code>test.aroundAll</code>  -  by <a href="https://github.com/MFA-G"><code>@​MFA-G</code></a> in <a href="">vitest-dev/eslint-plugin-vitest#959</a> <a href=""><!-- raw HTML omitted -->(8eb69)<!-- raw HTML omitted --></a></li>
<li><strong>prefer-comparison-matcher</strong>: Skip non-numeric operands with typecheck  -  by <a href="https://github.com/RagedPanda"><code>@​RagedPanda</code></a> in <a href="">vitest-dev/eslint-plugin-vitest#984</a> <a href=""><!-- raw HTML omitted -->(a6acf)<!-- raw HTML omitted --></a></li>
<li><strong>prefer-describe-function-title</strong>: Ignore type-only imports  -  by <a href="https://github.com/MFA-G"><code>@​MFA-G</code></a> in <a href="">vitest-dev/eslint-plugin-vitest#957</a> <a href=""><!-- raw HTML omitted -->(e2aaa)<!-- raw HTML omitted --></a></li>
<li><strong>prefer-spy-on</strong>: Pass an implementation to mockImplementation in the fix  -  by <a href="https://github.com/RaphaelFakhri"><code>@​RaphaelFakhri</code></a> in <a href="">vitest-dev/eslint-plugin-vitest#982</a> <a href=""><!-- raw HTML omitted -->(4c0ae)<!-- raw HTML omitted --></a></li>
<li><strong>unbound-method</strong>: Account for optional chaining  -  by <a href="https://github.com/G-Rath"><code>@​G-Rath</code></a> in <a href="">vitest-dev/eslint-plugin-vitest#975</a> <a href=""><!-- raw HTML omitted -->(743f8)<!-- raw HTML omitted --></a></li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/eslint-plugin-vitest/compare/v1.6.27...v1.6.28">View changes on GitHub</a></h5>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c5df105</code></a> chore: release v1.6.28</li>
<li><a href=""><code>8eb6991</code></a> fix(parse-vitest-fn-call): recognize member-form hooks like <code>test.aroundAll</code> ...</li>
<li><a href=""><code>e2aaac6</code></a> fix(prefer-describe-function-title): ignore type-only imports (<a href="">#957</a>)</li>
<li><a href=""><code>4c0ae5a</code></a> fix(prefer-spy-on): pass an implementation to mockImplementation in the fix (...</li>
<li><a href=""><code>a6acf78</code></a> fix(prefer-comparison-matcher): skip non-numeric operands with typecheck (<a href="">#984</a>)</li>
<li><a href=""><code>743f81f</code></a> fix(unbound-method): account for optional chaining (<a href="">#975</a>)</li>
<li><a href=""><code>8bdb180</code></a> docs: typo in prefer-to-contain rule docs (<a href="">#973</a>)</li>
<li><a href=""><code>0bea6e1</code></a> refactor(valid-expect): remove unneeded conditions and use optional chaining ...</li>
<li><a href=""><code>b3636d8</code></a> docs(consistent-test-it): fixed the description of the consistent-test-it opt...</li>
<li><a href=""><code>22d672a</code></a> chore: Update TypeScript version to v6 (<a href="">#945</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/vitest-dev/eslint-plugin-vitest/compare/v1.6.27...v1.6.28">compare view</a></li>
</ul>
</details>
<br />

Updates `eslint` from 10.12.0 to 10.13.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/eslint/eslint/releases">eslint's releases</a>.</em></p>
<blockquote>
<h2>v10.13.0</h2>
<h2>Features</h2>
<ul>
<li><a href=""><code>48d5cc4</code></a> feat: report references inside IIFEs in <code>no-use-before-define</code> (<a href="">#21238</a>) (Irfan fandi)</li>
<li><a href=""><code>a39d9fb</code></a> feat: add <code>globalThis</code> to <code>no-obj-calls</code> (<a href="">#21382</a>) (synthex-byte)</li>
<li><a href=""><code>66ac583</code></a> feat: check <code>yield*</code> expressions in <code>no-unsafe-optional-chaining</code> (<a href="">#21399</a>) (xbinaryx)</li>
</ul>
<h2>Bug Fixes</h2>
<ul>
<li><a href=""><code>87bd2ce</code></a> fix: avoid redeclared <code>let</code> when <code>no-var</code> and <code>one-var</code> fix together (<a href="">#21389</a>) (Daniel Pinto)</li>
</ul>
<h2>Documentation</h2>
<ul>
<li><a href=""><code>4783a68</code></a> docs: Update README (GitHub Actions Bot)</li>
<li><a href=""><code>43f0ac9</code></a> docs: clarify parameter description in <code>getText</code> (<a href="">#21287</a>) (lumir)</li>
</ul>
<h2>Chores</h2>
<ul>
<li><a href=""><code>b59d889</code></a> chore: update github/codeql-action action to v4.38.3 (<a href="">#21412</a>) (renovate[bot])</li>
<li><a href=""><code>95e51a0</code></a> ci: re-enable <code>@typescript-eslint/typescript-eslint</code> in ecosystem tests (<a href="">#21410</a>) (Francesco Trotta)</li>
<li><a href=""><code>317fcb3</code></a> chore: update ecosystem plugins (<a href="">#21409</a>) (ESLint Bot)</li>
<li><a href=""><code>b92decf</code></a> perf: skip no-redeclare scan for single-declaration variables (<a href="">#21365</a>) (James Ross)</li>
<li><a href=""><code>47b7063</code></a> chore: update dependency <code>@​eslint/json</code> to ^2.1.1 (<a href="">#21398</a>) (renovate[bot])</li>
<li><a href=""><code>e5aea41</code></a> chore: update ecosystem plugins (<a href="">#21390</a>) (ESLint Bot)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4637f98</code></a> 10.13.0</li>
<li><a href=""><code>96df05c</code></a> Build: changelog update for 10.13.0</li>
<li><a href=""><code>4783a68</code></a> docs: Update README</li>
<li><a href=""><code>b59d889</code></a> chore: update github/codeql-action action to v4.38.3 (<a href="">#21412</a>)</li>
<li><a href=""><code>95e51a0</code></a> ci: re-enable <code>@typescript-eslint/typescript-eslint</code> in ecosystem tests (<a href="">#21410</a>)</li>
<li><a href=""><code>317fcb3</code></a> chore: update ecosystem plugins (<a href="">#21409</a>)</li>
<li><a href=""><code>48d5cc4</code></a> feat: report references inside IIFEs in <code>no-use-before-define</code> (<a href="">#21238</a>)</li>
<li><a href=""><code>43f0ac9</code></a> docs: clarify parameter description in <code>getText</code> (<a href="">#21287</a>)</li>
<li><a href=""><code>a39d9fb</code></a> feat: add <code>globalThis</code> to <code>no-obj-calls</code> (<a href="">#21382</a>)</li>
<li><a href=""><code>b92decf</code></a> perf: skip no-redeclare scan for single-declaration variables (<a href="">#21365</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/eslint/eslint/compare/v10.12.0...v10.13.0">compare view</a></li>
</ul>
</details>
<br />

Updates `jsdom` from 30.1.2 to 30.1.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jsdom/jsdom/releases">jsdom's releases</a>.</em></p>
<blockquote>
<h2>v30.1.3</h2>
<ul>
<li>Improved performance of <code>getComputedStyle()</code> and computed CSS property reads, including with stylesheets containing attribute selectors. (<a href="https://github.com/scttcper"><code>@​scttcper</code></a>, <a href="https://github.com/asamuzaK"><code>@​asamuzaK</code></a>)</li>
<li>Fixed slowdowns when focusing elements and running interaction tests, which regressed in v30.1.2. (<a href="https://github.com/scttcper"><code>@​scttcper</code></a>)</li>
<li>Fixed <code>XMLHttpRequest</code> reusing credentials supplied to <code>xhr.open()</code> after cross-origin redirects, including in response to authentication challenges from the destination.</li>
<li>Fixed <code>XMLHttpRequest</code> incorrectly sending and accepting cookies after cross-origin redirects back to the document's origin when <code>xhr.withCredentials</code> is false.</li>
<li>Fixed exceptions from malformed CSS math functions, such as <code>calc(0px - @submenu_space)</code>, while parsing documents, stylesheets, and style declarations. (<a href="https://github.com/rnavarro"><code>@​rnavarro</code></a>)</li>
<li>Fixed <code>getComputedStyle()</code> ignoring style rules nested inside multiple <code>@media</code> rules.</li>
<li>Fixed CSS shorthands overwriting longhands with higher priority or specificity during style computation, including declarations containing CSS variables.</li>
<li>Fixed <code>getComputedStyle()</code> returning unresolved or inconsistent shorthand values, including for 'background', 'border', 'flex', 'font', 'margin', and 'padding', and incorrect shorthand defaults and inheritance.</li>
<li>Fixed computed background positions to resolve font-relative lengths using the final font size and handle multiple image layers correctly.</li>
<li>Fixed computed 'color' values depending on property read order, including unresolved <code>color-mix()</code> results, which regressed in v29.0.2.</li>
<li>Fixed <code>currentcolor</code> border colors incorrectly becoming transparent when 'color' uses <code>light-dark()</code> or relative color syntax.</li>
<li>Fixed CSS calculations that reduce to a percentage incorrectly producing pixel values, which regressed in v30.0.0.</li>
<li>Fixed numeric font weights in the 'font' shorthand incorrectly setting 'line-height'.</li>
<li>Fixed selector matching involving XML namespaces, and selectors such as <code>[data-a|=&quot;&quot;]</code> failing to match empty values and values beginning with <code>-</code>. (<a href="https://github.com/asamuzaK"><code>@​asamuzaK</code></a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>058c0f5</code></a> 30.1.3</li>
<li><a href=""><code>fcd1fd1</code></a> Cascade parsed longhands independently</li>
<li><a href=""><code>a3ee786</code></a> Cascade computed style properties on demand</li>
<li><a href=""><code>f42dc15</code></a> Resolve colors before caching or using currentcolor</li>
<li><a href=""><code>074b1fb</code></a> Compute background-position lengths against the final font size</li>
<li><a href=""><code>d19598c</code></a> Apply style rules nested in multiple <a href="https://github.com/media"><code>@​media</code></a> rules</li>
<li><a href=""><code>45d626c</code></a> Rule out attribute selector subjects before matching</li>
<li><a href=""><code>3ff0a5b</code></a> Upgrade Undici and remove abort workarounds</li>
<li><a href=""><code>8813bb1</code></a> Ignore CSS declarations with unparseable math functions</li>
<li><a href=""><code>63712d8</code></a> Fix XHR credentials across redirects</li>
<li>Additional commits viewable in <a href="https://github.com/jsdom/jsdom/compare/v30.1.2...v30.1.3">compare view</a></li>
</ul>
</details>
<br />

Updates `vite` from 8.3.4 to 8.3.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitejs/vite/releases">vite's releases</a>.</em></p>
<blockquote>
<h2>v8.3.5</h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>build:</strong> handle missing chunk import maps (<a href="">#23777</a>) (<a href="">8d7623d</a>)</li>
<li><strong>build:</strong> include preload dependencies to chunk import map hashing (<a href="">#23793</a>) (<a href="">4d16e7c</a>)</li>
<li><strong>bundled-dev:</strong> apply <code>server.origin</code> to asset URLs (<a href="">#23683</a>) (<a href="">52ba877</a>)</li>
<li><strong>bundled-dev:</strong> declare utf-8 charset in fallback page (<a href="">#23846</a>) (<a href="">197daf6</a>)</li>
<li><strong>bundled-dev:</strong> ignore build.chunkImportMap (<a href="">#23685</a>) (<a href="">cfe917d</a>)</li>
<li><strong>bundled-dev:</strong> include user <code>import.meta.env.*</code> defines in the <code>import.meta.env</code> object (<a href="">#23713</a>) (<a href="">6019aa7</a>)</li>
<li><strong>bundled-dev:</strong> map forwarded error stacks through the bundle source maps (<a href="">#23741</a>) (<a href="">11fe1e4</a>)</li>
<li><strong>bundled-dev:</strong> normalize served output files (<a href="">#23684</a>) (<a href="">df4e02c</a>)</li>
<li><strong>bundled-dev:</strong> stop hmr propagation at modules that are no longer imported (<a href="">#23839</a>) (<a href="">7471e8c</a>)</li>
<li><strong>css:</strong> don't fail on a literal <code>%</code> in <code>url()</code> (<a href="">#23676</a>) (<a href="">50b382d</a>)</li>
<li><strong>deps:</strong> update all non-major dependencies (<a href="">#23731</a>) (<a href="">cf80aa5</a>)</li>
<li><strong>deps:</strong> update all non-major dependencies (<a href="">#23826</a>) (<a href="">77d8373</a>)</li>
<li><strong>deps:</strong> update rolldown-related dependencies (<a href="">#23733</a>) (<a href="">43f0d05</a>)</li>
<li><strong>deps:</strong> update rolldown-related dependencies (<a href="">#23827</a>) (<a href="">c2e0418</a>)</li>
<li><strong>optimizer:</strong> fall back to yarn.lock for lockfile hash (<a href="">#23667</a>) (<a href="">f206096</a>)</li>
<li><strong>optimizer:</strong> scan <code>oxc.jsxInject</code> imports (<a href="">#23758</a>) (<a href="">38f3cb4</a>)</li>
<li><strong>optimizer:</strong> skip patches dir check for yarn.lock fallback (<a href="">#23725</a>) (<a href="">8e890e1</a>)</li>
<li><strong>optimizer:</strong> skip patches dir hash for nub lockfile (<a href="">#23761</a>) (<a href="">a7d5696</a>)</li>
<li><strong>resolve:</strong> support subpath imports with multiple <code>#</code> (<a href="">#23631</a>) (<a href="">0d86b34</a>)</li>
<li><strong>resolve:</strong> update resolve.exports to 2.0.4 (<a href="">#23739</a>) (<a href="">4ea708a</a>)</li>
<li><strong>server:</strong> handle socket errors on upgrade requests not taken by the HMR server (<a href="">#23728</a>) (<a href="">c2c9ef4</a>)</li>
<li><strong>server:</strong> only strip base when path matches a full segment (<a href="">#23641</a>) (<a href="">3dfde87</a>)</li>
</ul>
<h3>Performance Improvements</h3>
<ul>
<li><strong>ssr:</strong> extract inline source maps without a regexp (<a href="">#23775</a>) (<a href="">6a02780</a>)</li>
</ul>
<h3>Miscellaneous Chores</h3>
<ul>
<li>migrate to Oxlint (<a href="">#23746</a>) (<a href="">5b73935</a>)</li>
</ul>
<h3>Code Refactoring</h3>
<ul>
<li><strong>deps:</strong> replace <code>@vercel/detect-agent</code> with <code>std-env</code> (<a href="">#23744</a>) (<a href="">ce4293f</a>)</li>
<li><strong>dev:</strong> consolidate moduleURL to file path utilities (<a href="">#23828</a>) (<a href="">df7b40e</a>)</li>
<li><strong>dev:</strong> separate import resolution from URL conversion (<a href="">#23791</a>) (<a href="">6116689</a>)</li>
<li><strong>dev:</strong> share ModuleURL and BrowserURL conversions (<a href="">#23790</a>) (<a href="">446954c</a>)</li>
<li><strong>dev:</strong> use ModuleURLs throughout HTML transforms (<a href="">#23815</a>) (<a href="">a162990</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/vitejs/vite/blob/main/packages/vite/CHANGELOG.md">vite's changelog</a>.</em></p>
<blockquote>
<h2><!-- raw HTML omitted --><a href="https://github.com/vitejs/vite/compare/v8.3.4...v8.3.5">8.3.5</a> (2026-10-21)<!-- raw HTML omitted --></h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>build:</strong> handle missing chunk import maps (<a href="">#23777</a>) (<a href="">8d7623d</a>)</li>
<li><strong>build:</strong> include preload dependencies to chunk import map hashing (<a href="">#23793</a>) (<a href="">4d16e7c</a>)</li>
<li><strong>bundled-dev:</strong> apply <code>server.origin</code> to asset URLs (<a href="">#23683</a>) (<a href="">52ba877</a>)</li>
<li><strong>bundled-dev:</strong> declare utf-8 charset in fallback page (<a href="">#23846</a>) (<a href="">197daf6</a>)</li>
<li><strong>bundled-dev:</strong> ignore build.chunkImportMap (<a href="">#23685</a>) (<a href="">cfe917d</a>)</li>
<li><strong>bundled-dev:</strong> include user <code>import.meta.env.*</code> defines in the <code>import.meta.env</code> object (<a href="">#23713</a>) (<a href="">6019aa7</a>)</li>
<li><strong>bundled-dev:</strong> map forwarded error stacks through the bundle source maps (<a href="">#23741</a>) (<a href="">11fe1e4</a>)</li>
<li><strong>bundled-dev:</strong> normalize served output files (<a href="">#23684</a>) (<a href="">df4e02c</a>)</li>
<li><strong>bundled-dev:</strong> stop hmr propagation at modules that are no longer imported (<a href="">#23839</a>) (<a href="">7471e8c</a>)</li>
<li><strong>css:</strong> don't fail on a literal <code>%</code> in <code>url()</code> (<a href="">#23676</a>) (<a href="">50b382d</a>)</li>
<li><strong>deps:</strong> update all non-major dependencies (<a href="">#23731</a>) (<a href="">cf80aa5</a>)</li>
<li><strong>deps:</strong> update all non-major dependencies (<a href="">#23826</a>) (<a href="">77d8373</a>)</li>
<li><strong>deps:</strong> update rolldown-related dependencies (<a href="">#23733</a>) (<a href="">43f0d05</a>)</li>
<li><strong>deps:</strong> update rolldown-related dependencies (<a href="">#23827</a>) (<a href="">c2e0418</a>)</li>
<li><strong>optimizer:</strong> fall back to yarn.lock for lockfile hash (<a href="">#23667</a>) (<a href="">f206096</a>)</li>
<li><strong>optimizer:</strong> scan <code>oxc.jsxInject</code> imports (<a href="">#23758</a>) (<a href="">38f3cb4</a>)</li>
<li><strong>optimizer:</strong> skip patches dir check for yarn.lock fallback (<a href="">#23725</a>) (<a href="">8e890e1</a>)</li>
<li><strong>optimizer:</strong> skip patches dir hash for nub lockfile (<a href="">#23761</a>) (<a href="">a7d5696</a>)</li>
<li><strong>resolve:</strong> support subpath imports with multiple <code>#</code> (<a href="">#23631</a>) (<a href="">0d86b34</a>)</li>
<li><strong>resolve:</strong> update resolve.exports to 2.0.4 (<a href="">#23739</a>) (<a href="">4ea708a</a>)</li>
<li><strong>server:</strong> handle socket errors on upgrade requests not taken by the HMR server (<a href="">#23728</a>) (<a href="">c2c9ef4</a>)</li>
<li><strong>server:</strong> only strip base when path matches a full segment (<a href="">#23641</a>) (<a href="">3dfde87</a>)</li>
</ul>
<h3>Performance Improvements</h3>
<ul>
<li><strong>ssr:</strong> extract inline source maps without a regexp (<a href="">#23775</a>) (<a href="">6a02780</a>)</li>
</ul>
<h3>Miscellaneous Chores</h3>
<ul>
<li>migrate to Oxlint (<a href="">#23746</a>) (<a href="">5b73935</a>)</li>
</ul>
<h3>Code Refactoring</h3>
<ul>
<li><strong>deps:</strong> replace <code>@vercel/detect-agent</code> with <code>std-env</code> (<a href="">#23744</a>) (<a href="">ce4293f</a>)</li>
<li><strong>dev:</strong> consolidate moduleURL to file path utilities (<a href="">#23828</a>) (<a href="">df7b40e</a>)</li>
<li><strong>dev:</strong> separate import resolution from URL conversion (<a href="">#23791</a>) (<a href="">6116689</a>)</li>
<li><strong>dev:</strong> share ModuleURL and BrowserURL conversions (<a href="">#23790</a>) (<a href="">446954c</a>)</li>
<li><strong>dev:</strong> use ModuleURLs throughout HTML transforms (<a href="">#23815</a>) (<a href="">a162990</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>981f07f</code></a> release: v8.3.5 (<a href="">#23856</a>)</li>
<li><a href=""><code>0d86b34</code></a> fix(resolve): support subpath imports with multiple <code>#</code> (<a href="">#23631</a>)</li>
<li><a href=""><code>6a02780</code></a> perf(ssr): extract inline source maps without a regexp (<a href="">#23775</a>)</li>
<li><a href=""><code>8e890e1</code></a> fix(optimizer): skip patches dir check for yarn.lock fallback (<a href="">#23725</a>)</li>
<li><a href=""><code>197daf6</code></a> fix(bundled-dev): declare utf-8 charset in fallback page (<a href="">#23846</a>)</li>
<li><a href=""><code>4d16e7c</code></a> fix(build): include preload dependencies to chunk import map hashing (<a href="">#23793</a>)</li>
<li><a href=""><code>df7b40e</code></a> refactor(dev): consolidate moduleURL to file path utilities (<a href="">#23828</a>)</li>
<li><a href=""><code>a162990</code></a> refactor(dev): use ModuleURLs throughout HTML transforms (<a href="">#23815</a>)</li>
<li><a href=""><code>6116689</code></a> refactor(dev): separate import resolution from URL conversion (<a href="">#23791</a>)</li>
<li><a href=""><code>446954c</code></a> refactor(dev): share ModuleURL and BrowserURL conversions (<a href="">#23790</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/vitejs/vite/commits/v8.3.5/packages/vite">compare view</a></li>
</ul>
</details>
<br />

Updates `vitest` from 5.0.3 to 5.0.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitest-dev/vitest/releases">vitest's releases</a>.</em></p>
<blockquote>
<h2>v5.0.5</h2>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li>Keep vite default <code>fs.deny</code> with api token file  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11578</a> <a href=""><!-- raw HTML omitted -->(28dc1)<!-- raw HTML omitted --></a></li>
<li>Handle quoted file names in <code>--changed</code>  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11583</a> <a href=""><!-- raw HTML omitted -->(14921)<!-- raw HTML omitted --></a></li>
<li>Add <code>data</code> to the <code>import.meta.hot</code> stub  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11590</a> <a href=""><!-- raw HTML omitted -->(3a828)<!-- raw HTML omitted --></a></li>
<li>Set <code>skip</code> in <code>skipIf</code>, ignore <code>undefined</code> options  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11591</a> <a href=""><!-- raw HTML omitted -->(d523a)<!-- raw HTML omitted --></a></li>
<li>Skip builtin loading in async leak detector  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11598</a> <a href=""><!-- raw HTML omitted -->(fe86a)<!-- raw HTML omitted --></a></li>
<li>Keep the import frame in native loader errors  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11599</a> <a href=""><!-- raw HTML omitted -->(9697b)<!-- raw HTML omitted --></a></li>
<li>Run hook cleanups when a later hook fails  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11605</a> <a href=""><!-- raw HTML omitted -->(6c5a4)<!-- raw HTML omitted --></a></li>
<li>Release mocks of finished test files  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11607</a> <a href=""><!-- raw HTML omitted -->(e9c3d)<!-- raw HTML omitted --></a></li>
<li>Abort all running tests on cancel  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11606</a> <a href=""><!-- raw HTML omitted -->(6621a)<!-- raw HTML omitted --></a></li>
<li><strong>browser</strong>:
<ul>
<li>Ignore synthetic pagehide events  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11582</a> <a href=""><!-- raw HTML omitted -->(ca081)<!-- raw HTML omitted --></a></li>
<li>Run plugin buildStart on server creation  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11593</a> <a href=""><!-- raw HTML omitted -->(ea611)<!-- raw HTML omitted --></a></li>
<li>Drop late connections of closed sessions  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11600</a> <a href=""><!-- raw HTML omitted -->(f161e)<!-- raw HTML omitted --></a></li>
<li>Wait 30s for the browser to close  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11601</a> <a href=""><!-- raw HTML omitted -->(6498b)<!-- raw HTML omitted --></a></li>
<li>Run global setup once with instances  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11596</a> <a href=""><!-- raw HTML omitted -->(8dd67)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>reporter</strong>:
<ul>
<li>End reason <code>&amp;;failed&amp;;</code> on worker crash  -  by <a href="https://github.com/AriPerkkio"><code>@​AriPerkkio</code></a> in <a href="">vitest-dev/vitest#11568</a> <a href=""><!-- raw HTML omitted -->(6ae8e)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h5>    <a href="https://github.com/vitest-dev/vitest/compare/v5.0.4...v5.0.5">View changes on GitHub</a></h5>
<h2>v5.0.4</h2>
<h3>   🚀 Features</h3>
<ul>
<li><strong>experimental</strong>:
<ul>
<li>Tag cache directories with CACHEDIR.TAG  -  by <a href="https://github.com/lifeiscontent"><code>@​lifeiscontent</code></a> in <a href="">vitest-dev/vitest#11461</a> <a href=""><!-- raw HTML omitted -->(a8ea3)<!-- raw HTML omitted --></a></li>
<li>Support <code>test.ui.theme</code> option  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11499</a> <a href=""><!-- raw HTML omitted -->(1da66)<!-- raw HTML omitted --></a></li>
<li>Highlight selector multiple matches in trace view  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11489</a> <a href=""><!-- raw HTML omitted -->(5abba)<!-- raw HTML omitted --></a></li>
<li>Print how many tests were affected and a total when running <code>--changed</code>  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11424</a> <a href=""><!-- raw HTML omitted -->(a2336)<!-- raw HTML omitted --></a></li>
<li>Add an option to cache dependencies instead of statically parsing them  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11515</a> <a href=""><!-- raw HTML omitted -->(c0601)<!-- raw HTML omitted --></a></li>
<li>Add fit and zoom controls to trace viewer  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11490</a> <a href=""><!-- raw HTML omitted -->(f5dd9)<!-- raw HTML omitted --></a></li>
</ul>
</li>
</ul>
<h3>   🐞 Bug Fixes</h3>
<ul>
<li>Fail the run on git and location filter errors  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11430</a> <a href=""><!-- raw HTML omitted -->(30d03)<!-- raw HTML omitted --></a></li>
<li>Enable fsModuleCache by default  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11435</a> <a href=""><!-- raw HTML omitted -->(ad208)<!-- raw HTML omitted --></a></li>
<li>Track project files and mocks with --changed  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11432</a> <a href=""><!-- raw HTML omitted -->(b0f2b)<!-- raw HTML omitted --></a></li>
<li>Refactor caching, fix <code>:</code> in project and change the shape of <code>results</code> cache  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11453</a> <a href=""><!-- raw HTML omitted -->(9673c)<!-- raw HTML omitted --></a></li>
<li>Keep full <code>$</code> string values when <code>taskTitleValueFormatTruncate</code> is 0  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11485</a> <a href=""><!-- raw HTML omitted -->(4f7e1)<!-- raw HTML omitted --></a></li>
<li>Resolve node builtins in client environments  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11417</a> <a href=""><!-- raw HTML omitted -->(56b31)<!-- raw HTML omitted --></a></li>
<li>Fix module graph builtin externals after <a href="">#11421</a>  -  by <a href="https://github.com/hi-ogawa"><code>@​hi-ogawa</code></a>, <strong>Hiroshi Ogawa</strong> and <strong>Claude Opus 5.5</strong> in <a href="">vitest-dev/vitest#11491</a> and <a href="">vitest-dev/vitest#11421</a> <a href=""><!-- raw HTML omitted -->(008e1)<!-- raw HTML omitted --></a></li>
<li>Wrap module mocks during in-source testing  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11505</a> <a href=""><!-- raw HTML omitted -->(36d19)<!-- raw HTML omitted --></a></li>
<li>Handle line endings in snapshot  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11522</a> <a href=""><!-- raw HTML omitted -->(4c468)<!-- raw HTML omitted --></a></li>
<li>Respect root in projects  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11521</a> <a href=""><!-- raw HTML omitted -->(26642)<!-- raw HTML omitted --></a></li>
<li>Resolve mocks in directories with spaces  -  by <a href="https://github.com/sheremet-va"><code>@​sheremet-va</code></a> in <a href="">vitest-dev/vitest#11539</a> <a href=""><!-- raw HTML omitted -->(caaef)<!-- raw HTML omitted --></a></li>
<li><strong>api</strong>:
<ul>
<li>Publish the api token atomically  -  by <a href="https://github.com/umairnawaz333"><code>@​umairnawaz333</code></a> in <a href="">vitest-dev/vitest#11323</a> <a href=""><!-- raw HTML omitted -->(6f990)<!-- raw HTML omitted --></a></li>
</ul>
</li>
<li><strong>browser</strong>:</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7a825db</code></a> chore: release v5.0.5 (<a href="">#11609</a>)</li>
<li><a href=""><code>6621a72</code></a> fix: abort all running tests on cancel (<a href="">#11606</a>)</li>
<li><a href=""><code>e9c3d72</code></a> fix: release mocks of finished test files (<a href="">#11607</a>)</li>
<li><a href=""><code>8dd67c2</code></a> fix(browser): run global setup once with instances (<a href="">#11596</a>)</li>
<li><a href=""><code>6c5a447</code></a> fix: run hook cleanups when a later hook fails (<a href="">#11605</a>)</li>
<li><a href=""><code>9697b38</code></a> fix: keep the import frame in native loader errors (<a href="">#11599</a>)</li>
<li><a href=""><code>6498b66</code></a> fix(browser): ...

_Description has been truncated_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bdbf4232fce3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.