# Issue

**Title:** chore(deps): bump org.projectlombok:lombok from 1.18.30 to 1.18.46

## Description

Bumps [org.projectlombok:lombok](https://github.com/projectlombok/lombok) from 1.18.30 to 1.18.46.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/projectlombok/lombok/blob/master/doc/changelog.markdown">org.projectlombok:lombok's changelog</a>.</em></p>
<blockquote>
<h3>v1.18.46 (April 22nd, 2026)</h3>
<ul>
<li>PLATFORM: JDK26 support added <a href="">#4019</a>.</li>
<li>PLATFORM: Spring Tools Suite 5 supported <a href="">#3985</a>.</li>
<li>BUGFIX: <code>@Jacksonized</code> no longer stops generating <code>@JsonProperty</code> once an explicit <code>@JsonIgnore</code> annotations is encountered <a href="">#4022</a>.</li>
<li>BUGFIX: In eclipse, mixing <code>@Jacksonized</code> and <code>fluent = true</code> no longer causes the error <code>com.fasterxml.jackson.annotation.JsonProperty is not a repeatable annotation interface</code>. <a href="">#3934</a>.</li>
<li>BUGFIX: Some finishing touches for v1.18.44's support of Jackson3 <a href="">#4004</a>.</li>
</ul>
<h3>v1.18.44 (March 11th, 2026)</h3>
<ul>
<li>FEATURE: <code>@Jacksonized</code> now supports both Jackson2 and Jackson3; you'll get a warning until you configure which one (or even both!) you want lombok to generate. <a href="">#3950</a>.</li>
<li>BUGFIX: On JDK25, <code>val</code> and <code>@ExtensionMethod</code> could sometimes cause erroneous errors (in that you see errors but compilation succeeds anyway) using javac. <a href="">#3947</a>.</li>
<li>BUGFIX: <code>@Jacksonized</code> + fields marked <code>transient</code> would result in those transient fields being serialised which is surprising (and thus undesired) behaviour. <a href="">#3936</a>.</li>
</ul>
<h3>v1.18.42 (September 18th, 2025)</h3>
<ul>
<li>FEATURE: All the various <code>@Log</code> annotations now allow you to change their access level (they still default to <code>private</code>). <a href="">#2280</a>. Thanks to new contributor Liam Pace!</li>
<li>BUGFIX: Javadoc parsing was broken in Netbeans and ErrorProne for JDK25 <a href="">#3940</a>.</li>
</ul>
<h3>v1.18.40 (September 4th, 2025)</h3>
<ul>
<li>PLATFORM: JDK25 support added <a href="">#3859</a>.</li>
<li>BUGFIX: Recent versions of eclipse (or the eclipse-based java lang server for VSCode) caused <code>java.lang.IllegalArgumentException: Document does not match the AST</code>. [Issue <a href="">#3886</a>](<a href="">projectlombok/lombok#3886</a>).</li>
<li>PERFORMANCE: <code>@ExtensionMethod</code> is now significantly faster [Issue <a href="">#3866</a>](<a href="">projectlombok/lombok#3866</a>).</li>
<li>BUGFIX: the command line <code>config</code> tool would emit incorrect output for nullity annotations. [Issue <a href="">#3931</a>](<a href="">projectlombok/lombok#3931</a>).</li>
<li>FEATURE: <code>@Jacksonized @Accessors(fluent=true)</code> automatically creates the relevant annotations such that Jackson correctly identifies fluent accessors. [Issue <a href="">#3265</a>](<a href="">projectlombok/lombok#3265</a>), [Issue <a href="">#3270</a>](<a href="">projectlombok/lombok#3270</a>).</li>
<li>IMPROBABLE BREAKING CHANGE: From versions 1.18.16 to 1.18.38, lombok automatically copies certain Jackson annotations (e.g., <code>@JsonProperty</code>) from fields to the corresponding accessors (getters/setters). However, it turned out to be harmful in certain situations. Thus, Lombok does not automatically copy those annotations any more. You can restore the old behavior using the <a href="https://projectlombok.org/features/configuration">config key</a> <code>lombok.copyJacksonAnnotationsToAccessors = true</code>.</li>
</ul>
<h3>v1.18.38 (March 31st, 2025)</h3>
<ul>
<li>PLATFORM: JDK24 support added.</li>
<li>FEATURE: Lombok's nullity annotation now supports <a href="https://jspecify.dev">JSpecify</a> out of the box, using <a href="https://projectlombok.org/features/configuration">config key</a> <code>jspecify</code>.</li>
<li>BUGFIX: Recent eclipse releases would get you 'negative length' error. The bug had always been in lombok but didn't matter until recent releases. [Issue <a href="">#3823</a>](<a href="">projectlombok/lombok#3823</a>).</li>
<li>BUGFIX: The 'extract local variable' refactor script of VSCode wouldn't replace all occurrences if run on a method call to a lombok generated method. [Issue <a href="">#3783</a>](<a href="">projectlombok/lombok#3783</a>).</li>
</ul>
<h3>v1.18.36 (November 15th, 2024)</h3>
<ul>
<li>PLATFORM: JDK23 support added.</li>
<li>BUGFIX: Eclipse projects using the <code>com.pro-crafting.tools:jasperreports-maven-plugin</code> will now compile.</li>
</ul>
<h3>v1.18.34 (June 28th, 2024)</h3>
<ul>
<li>PLATFORM: Added support for Eclipse 2024-06; you'd get some <code>NoSuchMethodError</code> traces in your logs if using <code>@Builder</code> or <code>@Singular</code> prior to this fix. [Issue <a href="">#3638</a>](<a href="">projectlombok/lombok#3638</a>).</li>
<li>IMPROBABLE BREAKING CHANGE: Lombok now adds <code>@lombok.Generated</code> by default to methods and types it generates. This may result in accidentally increasing your test coverage percentage. [Issue <a href="">#3667</a>](<a href="">projectlombok/lombok#3667</a>).</li>
<li>IMPROBABLE BREAKING CHANGE: When <code>lombok.config</code> contains <code>lombok.onX.flagUsage = WARNING</code>, from now on warnings will actually be generated if onX is used.[Issue <a href="">#2848</a>](<a href="">projectlombok/lombok#2848</a>)</li>
<li>BUGFIX: When <code>@SuperBuilder</code> was used on a type with an generic array type, it would error <code>wrong number of type arguments</code>.  [Issue <a href="">#3694</a>](<a href="">projectlombok/lombok#3694</a>).</li>
<li>FEATURE: Lombok generates javadoc for you for most of the methods it adds; with this release, javadoc is also added to generated constructors. [Issue <a href="">#933</a>](<a href="">projectlombok/lombok#933</a>).</li>
</ul>
<h3>v1.18.32 (March 20th, 2024)</h3>
<ul>
<li>PLATFORM: Initial JDK22 support added.</li>
<li>PLAFTORM  Added support for Eclipse 2024-03. [Issue <a href="">#3620</a>](<a href="">projectlombok/lombok#3620</a>).</li>
<li>PLATFORM: Added support for recent versions of eclipse (released Q4 2023 or later or so) which would cause failures in the eclipse logs such as <code>java.lang.NoSuchMethodError: 'java.lang.StringBuffer org.eclipse.jdt…</code>. [Issue <a href="">#3564</a>](<a href="">projectlombok/lombok#3564</a>).</li>
<li>FEATURE: <code>@Locked</code> has been introduced. Like <code>@Synchronized</code> but with <code>java.util.concurrent.locks</code> locks instead of the <code>synchronized</code> primitive. Thanks, Pim van der Loos for the PR! [Issue <a href="">#3506</a>](<a href="">projectlombok/lombok#3506</a>).</li>
<li>NECROMANCY: Inlining a generated getter in eclipse would result in eclipse incorrectly replacing calls with <code>@Getter</code> instead of the actual field's name. [Issue <a href="">#562</a>](<a href="">projectlombok/lombok#562</a>). This issue is almost old enough to drink. Points for dedication go to Rawi for fixing this one.</li>
<li>BUGFIX: When <code>@SuperBuilder</code> was used on a type with an annotated generic type, it would error <code>wrong number of type arguments</code>.  [Issue <a href="">#3592</a>](<a href="">projectlombok/lombok#3592</a>).</li>
<li>BUGFIX: It was possible to create an infinite build loop using <code>@ExtensionMethod</code>. [Issue <a href="">#3225</a>](<a href="">projectlombok/lombok#3225</a>).</li>
<li>BUGFIX: Using <code>@Getter(lazy=true)</code> would fail if the expression contained a variable called <code>value</code>. [Issue <a href="">#2917</a>](<a href="">projectlombok/lombok#2917</a>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>936ca59</code></a> [build] lombok's launcher is still intended to be 1.4 compatible, or at least...</li>
<li><a href=""><code>fcdab3f</code></a> [version] pre-release version bump</li>
<li><a href=""><code>1cb7d49</code></a> [changelog]<a href="">#4004</a> Mention Jackson3 final touches in changelog.</li>
<li><a href=""><code>12a15b0</code></a> Fix: Bump EA_JDK to 27 (25 and 26 have been released)</li>
<li><a href=""><code>2be766c</code></a> Merge branch 'jackson3-final-touches'</li>
<li><a href=""><code>290fa4c</code></a> [trivial] constantize the warning we spit out for ambiguous jackson2/3, and m...</li>
<li><a href=""><code>e6567b6</code></a> test: Add Jackson 3 test cases and version ambiguity warnings</li>
<li><a href=""><code>45e72e2</code></a> feat: Add Jackson 3 databind/dataformat annotations to HandlerUtil copy lists</li>
<li><a href=""><code>184d423</code></a> feat: Add Jackson 3 support to <a href="https://github.com/Jacksonized"><code>@​Jacksonized</code></a> handlers</li>
<li><a href=""><code>e027ad0</code></a> refactored to ShadowClassLoader use Collections::enumeration instead of Vector</li>
<li>Additional commits viewable in <a href="https://github.com/projectlombok/lombok/compare/v1.18.30...v1.18.46">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.projectlombok:lombok&package-manager=gradle&previous-version=1.18.30&new-version=1.18.46)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b05a44306a0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.