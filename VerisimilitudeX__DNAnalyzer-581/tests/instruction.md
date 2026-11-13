# Issue

**Title:** chore(deps): bump com.google.guava:guava from 31.0.1-jre to 33.6.0-jre

## Description

Bumps [com.google.guava:guava](https://github.com/google/guava) from 31.0.1-jre to 33.6.0-jre.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/google/guava/releases">com.google.guava:guava's releases</a>.</em></p>
<blockquote>
<h2>33.6.0</h2>
<h3>Maven</h3>
<pre lang="xml"><code>&lt;dependency&gt;
  &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
  &lt;artifactId&gt;guava&lt;/artifactId&gt;
  &lt;version&gt;33.6.0-jre&lt;/version&gt;
  &lt;!-- or, for Android: --&gt;
  &lt;version&gt;33.6.0-android&lt;/version&gt;
&lt;/dependency&gt;
</code></pre>
<h3>Jar files</h3>
<ul>
<li><a href="https://repo1.maven.org/maven2/com/google/guava/guava/33.6.0-jre/guava-33.6.0-jre.jar">33.6.0-jre.jar</a></li>
<li><a href="https://repo1.maven.org/maven2/com/google/guava/guava/33.6.0-android/guava-33.6.0-android.jar">33.6.0-android.jar</a></li>
</ul>
<p>Guava requires <a href="https://github.com/google/guava/wiki/UseGuavaInYourBuild#what-about-guavas-own-dependencies">one runtime dependency</a>, which you can download here:</p>
<ul>
<li><a href="https://repo1.maven.org/maven2/com/google/guava/failureaccess/1.0.3/failureaccess-1.0.3.jar">failureaccess-1.0.3.jar</a></li>
</ul>
<h3>Javadoc</h3>
<ul>
<li><a href="https://guava.dev/releases/33.6.0-jre/api/docs/">33.6.0-jre</a></li>
<li><a href="https://guava.dev/releases/33.6.0-android/api/docs/">33.6.0-android</a></li>
</ul>
<h3>JDiff</h3>
<ul>
<li><a href="https://guava.dev/releases/33.6.0-jre/api/diffs/">33.6.0-jre vs. 33.5.0-jre</a></li>
<li><a href="https://guava.dev/releases/33.6.0-android/api/diffs/">33.6.0-android vs. 33.5.0-android</a></li>
<li><a href="https://guava.dev/releases/33.6.0-android/api/androiddiffs/">33.6.0-android vs. 33.6.0-jre</a></li>
</ul>
<h3>Changelog</h3>
<ul>
<li>Migrated some classes from <code>finalize()</code> to <code>PhantomReference</code> in preparation for <a href="https://openjdk.org/jeps/421">the removal of finalization</a>. (786b619dd6, 7c6b17c, aeef90988d)</li>
<li><code>cache</code>: Deprecated <code>CacheBuilder</code> APIs that use <code>TimeUnit</code> in favor of those that use <code>Duration</code>. (73f8b0bb84)</li>
<li><code>collect</code>: Added <code>toImmutableSortedMap</code> collectors that use the natural comparator. (64d70b9f94)</li>
<li><code>collect</code>: Changed <code>ConcurrentHashMultiset</code>, <code>ImmutableMap</code> and <code>TreeMultiset</code> deserialization to <a href="https://openjdk.org/jeps/500">avoid mutating <code>final</code> fields</a>. In extremely unlikely scenarios in which an instance of that type contains an object that refers back to that instance, this could lead to <a href="https://docs.oracle.com/en/java/javase/26/docs/specs/serialization/input.html#the-readresolve-method:~:text=in%20cases%20where%20an%20object%20being%20serialized%20nominates%20a%20replacement%20object%20whose%20object%20graph%20has%20a%20reference%20to%20the%20original%20object">a broken instance</a> that throws <code>NullPointerException</code> when used. (8240c7e596, 046468055f)</li>
<li><code>graph</code>: Removed <code>@Beta</code> from all APIs in the package. (dae9566b73)</li>
<li><code>graph</code>: Added support to <code>Graphs.transitiveClosure()</code> for different strategies for adding self-loops. (2e13df25b2)</li>
<li><code>graph</code>: Added an <code>asNetwork()</code> view to <code>Graph</code> and <code>ValueGraph</code>. (909c593c61)</li>
<li><code>hash</code>: Added <code>BloomFilter.serializedSize()</code>. (df9bcc251a)</li>
<li><code>net</code>: Added <code>HttpHeaders.CDN_CACHE_CONTROL</code>. (75331b5030)</li>
</ul>
<h2>33.5.0</h2>
<h3>Maven</h3>
<pre lang="xml"><code>&lt;dependency&gt;
&lt;/tr&gt;&lt;/table&gt;
</code></pre>
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/google/guava/commits">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.google.guava:guava&package-manager=gradle&previous-version=31.0.1-jre&new-version=33.6.0-jre)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68d69c6a7a0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.