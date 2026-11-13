# Issue

**Title:** Bump @vue/server-renderer and vue in /docs

## Description

Bumps [@vue/server-renderer](https://github.com/vuejs/core/tree/HEAD/packages/server-renderer) and [vue](https://github.com/vuejs/core). These dependencies needed to be updated together.
Updates `@vue/server-renderer` from 3.5.21 to 3.5.44
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vuejs/core/releases">@​vue/server-renderer's releases</a>.</em></p>
<blockquote>
<h2>v3.5.44</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.43</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.42</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.41</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.40</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.39</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.38</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.37</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.35</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.34</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.33</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.32</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.31</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">@​vue/server-renderer's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/vuejs/core/compare/v3.5.43...v3.5.44">3.5.44</a> (2026-10-13)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>compat:</strong> expose _setupProxy for Vue 2.7 compiled script setup (fix <a href="">#11164</a>) (<a href="">#15618</a>) (<a href="">f08059d</a>)</li>
<li><strong>compiler-core:</strong> parenthesise v-for key in v-memo cache guard (<a href="">#15724</a>) (<a href="">d084b90</a>), closes <a href="">#15723</a></li>
<li><strong>compiler-dom:</strong> correctly stringify <code>0</code> and <code>false</code> in <code>v-html</code> (<a href="">#15571</a>) (<a href="">9f3b437</a>)</li>
<li><strong>compiler-dom:</strong> inject transition persisted for v-show in production (<a href="">#15783</a>) (<a href="">89cb272</a>)</li>
<li><strong>compiler-sfc:</strong> error when defineModel prop options reference a destructured prop (<a href="">#15604</a>) (<a href="">38012a5</a>), closes <a href="">#15602</a></li>
<li><strong>custom-element:</strong> skip mounting an async custom element removed while its component loads (<a href="">#15777</a>) (<a href="">0f8e7b4</a>), closes <a href="">#15775</a></li>
<li><strong>hydration:</strong> observe children of a display: contents root in hydrateOnVisible (<a href="">#15773</a>) (<a href="">7f688e8</a>)</li>
<li><strong>KeepAlive:</strong> unmount pruned current component when its vnode was cloned on mount (<a href="">#15711</a>) (<a href="">92798ac</a>), closes <a href="">#15710</a></li>
<li><strong>reactivity:</strong> avoid mutating native array iterators (<a href="">#15703</a>) (<a href="">7f9d45d</a>), closes <a href="">#15643</a></li>
<li><strong>reactivity:</strong> do not track deps in watcher callbacks run inside another effect (<a href="">#15782</a>) (<a href="">db00fe9</a>), closes <a href="">#5009</a></li>
<li><strong>reactivity:</strong> once watcher should stop when its callback throws (<a href="">#15755</a>) (<a href="">ae4bd94</a>)</li>
<li><strong>reactivity:</strong> preserve shallow collection semantics (<a href="">#15793</a>) (<a href="">b600466</a>), closes <a href="">#15792</a></li>
<li><strong>runtime-core:</strong> detect new prop keys when comparing full props (<a href="">#15634</a>) (<a href="">702fa61</a>), closes <a href="">#15632</a></li>
<li><strong>runtime-core:</strong> keep async placeholder for block patching and pending component updates (<a href="">#15554</a>) (<a href="">05ec25f</a>), closes <a href="">#15551</a></li>
<li><strong>runtime-core:</strong> only flush jobs queued by the root render itself (<a href="">#15757</a>) (<a href="">0bea14b</a>), closes <a href="">#6728</a></li>
<li><strong>runtime-core:</strong> render nothing for an invalid v-for range in production (<a href="">#15742</a>) (<a href="">ad19e7d</a>)</li>
<li><strong>runtime-dom:</strong> preserve v-show display for unchanged style strings (<a href="">#15794</a>) (<a href="">c0a6d3f</a>)</li>
<li><strong>runtime-dom:</strong> treat playsinline as a boolean attribute (<a href="">#15627</a>) (<a href="">a084e44</a>)</li>
<li><strong>server-renderer:</strong> propagate async setup errors (<a href="">#15857</a>) (<a href="">6930374</a>), closes <a href="">#15716</a></li>
<li><strong>ssr:</strong> honor falsy vnode content overrides (<a href="">#15769</a>) (<a href="">c11c5c8</a>)</li>
<li><strong>suspense:</strong> mount resolved async component with its own namespace (<a href="">#15640</a>) (<a href="">2a086a2</a>), closes <a href="">#15639</a></li>
<li><strong>suspense:</strong> skip rendering async components unmounted while pending (<a href="">4ab865a</a>)</li>
<li><strong>teleport:</strong> move targetStart and keep children before targetAnchor (<a href="">#15818</a>) (<a href="">d3c6e02</a>), closes <a href="">#15817</a></li>
<li><strong>transition-group:</strong> measure nested groups against their moving outer item (<a href="">#15848</a>) (<a href="">1936c87</a>), closes <a href="">#5385</a> <a href="">#1531</a></li>
<li><strong>transition:</strong> handle comment-wrapped component roots (<a href="">#15853</a>) (<a href="">ff35014</a>), closes <a href="">#6080</a> <a href="">#5500</a></li>
</ul>
<h2><a href="https://github.com/vuejs/core/compare/v3.5.42...v3.5.43">3.5.43</a> (2026-09-17)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>compiler-sfc:</strong> ignore comment delimiters inside strings and url() when parsing css vars (<a href="">#15548</a>) (<a href="">2fde323</a>)</li>
<li><strong>compiler-sfc:</strong> prepend semicolon for await in switch case (<a href="">#15498</a>) (<a href="">9a1df69</a>), closes <a href="">#15495</a></li>
<li><strong>compiler-sfc:</strong> restore await scope when leaving nested blocks (<a href="">5409708</a>), closes <a href="">#15465</a></li>
<li><strong>compiler-sfc:</strong> reuse parsed parent configs across tsconfig walks (fix <a href="">#15478</a>) (<a href="">#15480</a>) (<a href="">d6febaa</a>)</li>
<li><strong>hydration:</strong> run leave hooks for hydration placeholders (<a href="">#15431</a>) (<a href="">5dda192</a>)</li>
<li><strong>reactivity:</strong> preserve readonly wrappers in array copy methods (<a href="">#15469</a>) (<a href="">599f35b</a>)</li>
<li><strong>runtime-core:</strong> unmount v-once children after parent rerenders (<a href="">#15435</a>) (<a href="">d720338</a>)</li>
<li><strong>shared:</strong> handle circular references in looseEqual (<a href="">#15499</a>) (<a href="">718f782</a>), closes <a href="">#15496</a></li>
<li><strong>shared:</strong> preserve comment-like text in style values (<a href="">#15471</a>) (<a href="">b9456cb</a>)</li>
<li><strong>suspense:</strong> don't drop nested suspense patches during hydration (<a href="">#15429</a>) (<a href="">76d42dc</a>)</li>
<li><strong>suspense:</strong> keep the boundary pending while its branch is patched (<a href="">#15411</a>) (<a href="">bfcfe9e</a>), closes <a href="">#7506</a></li>
<li><strong>suspense:</strong> patch a hydrating boundary's pending branch in place (<a href="">#15432</a>) (<a href="">2cde6f7</a>)</li>
<li><strong>suspense:</strong> unmount the DOM an interrupted async component claimed (<a href="">#15430</a>) (<a href="">fb9b45c</a>)</li>
<li><strong>types:</strong> keep optional props when a runtime prop uses a generic PropType (<a href="">#15523</a>) (<a href="">243aabc</a>), closes <a href="">#9546</a></li>
</ul>
<h2><a href="https://github.com/vuejs/core/compare/v3.5.41...v3.5.42">3.5.42</a> (2026-08-27)</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bf5f0dd</code></a> release: v3.5.44</li>
<li><a href=""><code>6930374</code></a> fix(server-renderer): propagate async setup errors (<a href="">#15857</a>)</li>
<li><a href=""><code>c11c5c8</code></a> fix(ssr): honor falsy vnode content overrides (<a href="">#15769</a>)</li>
<li><a href=""><code>ad19e7d</code></a> fix(runtime-core): render nothing for an invalid v-for range in production (#...</li>
<li><a href=""><code>a084e44</code></a> fix(runtime-dom): treat playsinline as a boolean attribute (<a href="">#15627</a>)</li>
<li><a href=""><code>5be58b4</code></a> release: v3.5.43</li>
<li><a href=""><code>d63616c</code></a> release: v3.5.42</li>
<li><a href=""><code>a2b40db</code></a> fix(server-renderer): reject CR in attribute names (<a href="">#15266</a>)</li>
<li><a href=""><code>d2c458b</code></a> release: v3.5.41</li>
<li><a href=""><code>4e467d7</code></a> fix(ssr): normalize hidden states during hydration (<a href="">#13125</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/vuejs/core/commits/v3.5.44/packages/server-renderer">compare view</a></li>
</ul>
</details>
<br />

Updates `vue` from 3.5.21 to 3.5.44
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vuejs/core/releases">vue's releases</a>.</em></p>
<blockquote>
<h2>v3.5.44</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.43</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.42</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.41</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.40</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.39</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.38</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.37</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.35</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.34</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.33</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.32</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.
For pre-releases, please refer to <a href="https://github.com/vuejs/core/blob/minor/CHANGELOG.md">CHANGELOG.md</a> of the <code>minor</code> branch.</p>
<h2>v3.5.31</h2>
<p>For stable releases, please refer to <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">CHANGELOG.md</a> for details.</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/vuejs/core/blob/main/CHANGELOG.md">vue's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/vuejs/core/compare/v3.5.43...v3.5.44">3.5.44</a> (2026-10-13)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>compat:</strong> expose _setupProxy for Vue 2.7 compiled script setup (fix <a href="">#11164</a>) (<a href="">#15618</a>) (<a href="">f08059d</a>)</li>
<li><strong>compiler-core:</strong> parenthesise v-for key in v-memo cache guard (<a href="">#15724</a>) (<a href="">d084b90</a>), closes <a href="">#15723</a></li>
<li><strong>compiler-dom:</strong> correctly stringify <code>0</code> and <code>false</code> in <code>v-html</code> (<a href="">#15571</a>) (<a href="">9f3b437</a>)</li>
<li><strong>compiler-dom:</strong> inject transition persisted for v-show in production (<a href="">#15783</a>) (<a href="">89cb272</a>)</li>
<li><strong>compiler-sfc:</strong> error when defineModel prop options reference a destructured prop (<a href="">#15604</a>) (<a href="">38012a5</a>), closes <a href="">#15602</a></li>
<li><strong>custom-element:</strong> skip mounting an async custom element removed while its component loads (<a href="">#15777</a>) (<a href="">0f8e7b4</a>), closes <a href="">#15775</a></li>
<li><strong>hydration:</strong> observe children of a display: contents root in hydrateOnVisible (<a href="">#15773</a>) (<a href="">7f688e8</a>)</li>
<li><strong>KeepAlive:</strong> unmount pruned current component when its vnode was cloned on mount (<a href="">#15711</a>) (<a href="">92798ac</a>), closes <a href="">#15710</a></li>
<li><strong>reactivity:</strong> avoid mutating native array iterators (<a href="">#15703</a>) (<a href="">7f9d45d</a>), closes <a href="">#15643</a></li>
<li><strong>reactivity:</strong> do not track deps in watcher callbacks run inside another effect (<a href="">#15782</a>) (<a href="">db00fe9</a>), closes <a href="">#5009</a></li>
<li><strong>reactivity:</strong> once watcher should stop when its callback throws (<a href="">#15755</a>) (<a href="">ae4bd94</a>)</li>
<li><strong>reactivity:</strong> preserve shallow collection semantics (<a href="">#15793</a>) (<a href="">b600466</a>), closes <a href="">#15792</a></li>
<li><strong>runtime-core:</strong> detect new prop keys when comparing full props (<a href="">#15634</a>) (<a href="">702fa61</a>), closes <a href="">#15632</a></li>
<li><strong>runtime-core:</strong> keep async placeholder for block patching and pending component updates (<a href="">#15554</a>) (<a href="">05ec25f</a>), closes <a href="">#15551</a></li>
<li><strong>runtime-core:</strong> only flush jobs queued by the root render itself (<a href="">#15757</a>) (<a href="">0bea14b</a>), closes <a href="">#6728</a></li>
<li><strong>runtime-core:</strong> render nothing for an invalid v-for range in production (<a href="">#15742</a>) (<a href="">ad19e7d</a>)</li>
<li><strong>runtime-dom:</strong> preserve v-show display for unchanged style strings (<a href="">#15794</a>) (<a href="">c0a6d3f</a>)</li>
<li><strong>runtime-dom:</strong> treat playsinline as a boolean attribute (<a href="">#15627</a>) (<a href="">a084e44</a>)</li>
<li><strong>server-renderer:</strong> propagate async setup errors (<a href="">#15857</a>) (<a href="">6930374</a>), closes <a href="">#15716</a></li>
<li><strong>ssr:</strong> honor falsy vnode content overrides (<a href="">#15769</a>) (<a href="">c11c5c8</a>)</li>
<li><strong>suspense:</strong> mount resolved async component with its own namespace (<a href="">#15640</a>) (<a href="">2a086a2</a>), closes <a href="">#15639</a></li>
<li><strong>suspense:</strong> skip rendering async components unmounted while pending (<a href="">4ab865a</a>)</li>
<li><strong>teleport:</strong> move targetStart and keep children before targetAnchor (<a href="">#15818</a>) (<a href="">d3c6e02</a>), closes <a href="">#15817</a></li>
<li><strong>transition-group:</strong> measure nested groups against their moving outer item (<a href="">#15848</a>) (<a href="">1936c87</a>), closes <a href="">#5385</a> <a href="">#1531</a></li>
<li><strong>transition:</strong> handle comment-wrapped component roots (<a href="">#15853</a>) (<a href="">ff35014</a>), closes <a href="">#6080</a> <a href="">#5500</a></li>
</ul>
<h2><a href="https://github.com/vuejs/core/compare/v3.5.42...v3.5.43">3.5.43</a> (2026-09-17)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>compiler-sfc:</strong> ignore comment delimiters inside strings and url() when parsing css vars (<a href="">#15548</a>) (<a href="">2fde323</a>)</li>
<li><strong>compiler-sfc:</strong> prepend semicolon for await in switch case (<a href="">#15498</a>) (<a href="">9a1df69</a>), closes <a href="">#15495</a></li>
<li><strong>compiler-sfc:</strong> restore await scope when leaving nested blocks (<a href="">5409708</a>), closes <a href="">#15465</a></li>
<li><strong>compiler-sfc:</strong> reuse parsed parent configs across tsconfig walks (fix <a href="">#15478</a>) (<a href="">#15480</a>) (<a href="">d6febaa</a>)</li>
<li><strong>hydration:</strong> run leave hooks for hydration placeholders (<a href="">#15431</a>) (<a href="">5dda192</a>)</li>
<li><strong>reactivity:</strong> preserve readonly wrappers in array copy methods (<a href="">#15469</a>) (<a href="">599f35b</a>)</li>
<li><strong>runtime-core:</strong> unmount v-once children after parent rerenders (<a href="">#15435</a>) (<a href="">d720338</a>)</li>
<li><strong>shared:</strong> handle circular references in looseEqual (<a href="">#15499</a>) (<a href="">718f782</a>), closes <a href="">#15496</a></li>
<li><strong>shared:</strong> preserve comment-like text in style values (<a href="">#15471</a>) (<a href="">b9456cb</a>)</li>
<li><strong>suspense:</strong> don't drop nested suspense patches during hydration (<a href="">#15429</a>) (<a href="">76d42dc</a>)</li>
<li><strong>suspense:</strong> keep the boundary pending while its branch is patched (<a href="">#15411</a>) (<a href="">bfcfe9e</a>), closes <a href="">#7506</a></li>
<li><strong>suspense:</strong> patch a hydrating boundary's pending branch in place (<a href="">#15432</a>) (<a href="">2cde6f7</a>)</li>
<li><strong>suspense:</strong> unmount the DOM an interrupted async component claimed (<a href="">#15430</a>) (<a href="">fb9b45c</a>)</li>
<li><strong>types:</strong> keep optional props when a runtime prop uses a generic PropType (<a href="">#15523</a>) (<a href="">243aabc</a>), closes <a href="">#9546</a></li>
</ul>
<h2><a href="https://github.com/vuejs/core/compare/v3.5.41...v3.5.42">3.5.42</a> (2026-08-27)</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bf5f0dd</code></a> release: v3.5.44</li>
<li><a href=""><code>6930374</code></a> fix(server-renderer): propagate async setup errors (<a href="">#15857</a>)</li>
<li><a href=""><code>8e8c547</code></a> chore(deps): update all non-major dependencies (<a href="">#15585</a>)</li>
<li><a href=""><code>4cb0ca8</code></a> chore(deps): update playground (<a href="">#15685</a>)</li>
<li><a href=""><code>e38478f</code></a> chore(deps): update dawidd6/action-download-artifact action to v27 (<a href="">#15768</a>)</li>
<li><a href=""><code>1caed5a</code></a> chore(deps): update compiler (<a href="">#15586</a>)</li>
<li><a href=""><code>a49f451</code></a> chore(deps): update lint (<a href="">#15680</a>)</li>
<li><a href=""><code>219b858</code></a> chore(deps): update build (<a href="">#15679</a>)</li>
<li><a href=""><code>ff35014</code></a> fix(transition): handle comment-wrapped component roots (<a href="">#15853</a>)</li>
<li><a href=""><code>d084b90</code></a> fix(compiler-core): parenthesise v-for key in v-memo cache guard (<a href="">#15724</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/vuejs/core/compare/v3.5.21...v3.5.44">compare view</a></li>
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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/gear-genomics/tracy/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bd0b322ca23`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.