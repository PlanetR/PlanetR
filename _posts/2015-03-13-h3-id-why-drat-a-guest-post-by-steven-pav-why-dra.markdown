---
title: "&lt;h3 id=&quot;why-drat-a-guest-post-by-steven-pav&quot;&gt;Why Drat? A Guest Post by Steven Pav&lt;/h3&gt;"
kind: article
created_at: 2015-03-13 23:49:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p><em>Editorial Note: The following post was kindly contributed by <a href="https://twitter.com/shabbychef">Steven Pav</a>.</em></p>
<h3 id="why-drat">Why Drat?</h3>
<p>After playing around with <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> for a few days now, my impressions of it are best captured by Dirk's quote:</p>
<blockquote>
<p>It just works.</p>
</blockquote>
<h4 id="demo">Demo</h4>
<p>To get some idea of what I mean by this, suppose you are a happy consumer of R packages, but want access to, say, the latest, greatest releases of my distribution package, <a href="https://github.com/shabbychef/sadists">sadist</a>. You can simply add the following to your <code>.Rprofile</code> file:</p>
<pre class="sourceCode r"><code class="sourceCode r">drat:::<span class="kw">add</span>(<span class="st">&quot;shabbychef&quot;</span>)</code></pre>
<p>After this, you instantly have access to new releases in the <a href="https://github.com/shabbychef/drat/tree/gh-pages">github/shabbychef drat store</a> via the package tools you already know and tolerate. You can use</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">install.packages</span>(<span class="st">&#39;sadists&#39;</span>)</code></pre>
<p>to install the sadists package from the drat store, for example. Similarly, if you issue</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">update.packages</span>(<span class="dt">ask=</span><span class="ot">FALSE</span>)</code></pre>
<p>all the drat stores you have added will be checked for package updates, along with their dependencies which may well come from other repositories including CRAN.</p>
<h4 id="use-cases">Use cases</h4>
<p>The most obvious use cases are:</p>
<ol style="list-style-type: decimal">
<li><p>Micro releases. For package authors, this provides a means to get feedback from the early adopters, but also allows one to push small changes and bug fixes without burning through your CRAN karma (if you have any left). My personal drat store tends to be a few minor releases ahead of my CRAN releases.</p></li>
<li><p>Local repositories. In my professional life, I write and maintain proprietary packages. Pushing package updates used to involve saving the package .tar.gz to a NAS, then calling something like <code>R CMD INSTALL package_name_0.3.1.9001.tar.gz</code>. This is not something I wanted to ask of my colleagues. With drat, they can instead add the following stanza to .Rprofile: <code>drat:::addRepo('localRepo','file:///mnt/NAS/r/local/drat')</code>, and then rely on <code>update.packages</code> to do the rest.</p></li>
</ol>
<p>I suspect that in the future, <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> might be (ab)used in the following ways:</p>
<ol start="3" style="list-style-type: decimal">
<li><p>Rolling your own vanilla CRAN mirror, though I suspect there are better existing ways to accomplish this.</p></li>
<li><p>Patching CRAN. Suppose you found a bug in a package on CRAN (inconceivable!). As it stands now, you email the maintainer, and wait for a fix. Maybe the patch is trivial, but suppose it is never delivered. Now, you can simply make the patch yourself, pick a higher revision number, and stash it in your drat store. The only downside is that eventually the package maintainer might bump their revision number without pushing a fix, and you are stuck in an arms race of version numbers.</p></li>
<li><p>Forgoing CRAN altogether. While some package maintainers might find this attractive, I think I would prefer a single huge repository, warts and all, to a landscape of a million microrepos. Perhaps some enterprising group will set up a CRAN-like drat store on github, and accept packages by pull request (whether github CDN can or will support the traffic that CRAN does is another matter), but this seems a bit too futuristic for me now.</p></li>
</ol>
<h4 id="my-wish-list">My wish list</h4>
<p>In exchange for writing this blog post, I get to lobby Dirk for some features in drat:</p>
<ol start="6" style="list-style-type: decimal">
<li><p>I shudder at the thought of hundreds of tiny drat stores. Perhaps there should be a way to aggregate <code>addRepo</code> commands in some way. This would allow curators to publish their suggested lists of repos.</p></li>
<li><p>Drat stores are served in the <code>gh-pages</code> branch of a github repo. I wish there were some way to keep the index.html file in that directory reflect the packages present in the sources. Maybe this could be achieved with some canonical RMarkdown code that most people use.</p></li>
</ol>
<p style="font-size:80%; font-style:italic;">
<strong>Update:</strong>Two typos fixed in code examples on 2015-Mar-27.
</p>

<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
