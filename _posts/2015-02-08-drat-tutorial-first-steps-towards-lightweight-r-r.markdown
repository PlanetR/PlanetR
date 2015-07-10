---
title: "drat Tutorial: First Steps towards Lightweight R Repositories"
kind: article
created_at: 2015-02-08 00:01:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>Now that <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> is on <a href="http://cran.r-project.org">CRAN</a> and I got a bit of feedback (or typo corrections) in three issue tickets, I thought I could show how to quickly post such an interim version in a <em>drat</em> repository.</p>
<p>Now, I obviously already have a checkout of <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>. If you, dear reader, wanted to play along and create your own <em>drat</em> repository, one rather simple way would be to simply clone my repo as this gets you the desired <code>gh-pages</code> branch with the required <code>src/contrib/</code> directories. Otherwise just do it by hand.</p>
<p>Back to a new interim version. I just pushed commit <a href="https://github.com/eddelbuettel/drat/commit/fd06293c2151a13b026196575d0dd20938c01f58">fd06293</a> which bumps the version and date for the new interim release based mostly on the three tickets addresses right after the <a href="http://dirk.eddelbuettel.com/blog/2015/02/05#drat_0.0.1">initial release 0.0.1</a>. So by building it we get a new version 0.0.1.1:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ R CMD build drat
<span class="kw">*</span> checking for file ‘drat/DESCRIPTION’ ... OK
<span class="kw">*</span> preparing ‘drat’:
<span class="kw">*</span> checking DESCRIPTION meta-information ... OK
<span class="kw">*</span> checking for LF line-endings in source and make files
<span class="kw">*</span> checking for empty or unneeded directories
<span class="kw">*</span> building ‘drat_0.0.1.1.tar.gz’

<span class="kw">edd@max</span>:~/git$ </code></pre>
<p>Because I want to use the <code>drat</code> repo next, I need to now switch from <code>master</code> to <code>gh-pages</code>; a step I am omitting as we can assume that your <code>drat</code> repo will already be on its <code>gh-pages</code> branch.</p>
<p>Next we simply call the <code>drat</code> function to add the release:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ r -e <span class="st">&#39;drat:::insert(&quot;drat_0.0.1.1.tar.gz&quot;)&#39;</span>
<span class="kw">edd@max</span>:~/git$ </code></pre>
<p>As expected, now have two updated <code>PACKAGES</code> files (compressed and plain) and a new tarball:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git/drat(gh-pages)$ <span class="kw">git</span> status
<span class="kw">On</span> branch gh-pages
<span class="kw">Your</span> branch is up-to-date with <span class="st">&#39;origin/gh-pages&#39;</span>.
<span class="kw">Changes</span> not staged for commit:
  <span class="kw">(use</span> <span class="st">&quot;git add &lt;file&gt;...&quot;</span> to update what will be committed<span class="kw">)</span>
  <span class="kw">(use</span> <span class="st">&quot;git checkout -- &lt;file&gt;...&quot;</span> to discard changes in working directory<span class="kw">)</span>

        <span class="kw">modified</span>:   src/contrib/PACKAGES
        <span class="kw">modified</span>:   src/contrib/PACKAGES.gz

<span class="kw">Untracked</span> files:
  <span class="kw">(use</span> <span class="st">&quot;git add &lt;file&gt;...&quot;</span> to include in what will be committed<span class="kw">)</span>

        <span class="kw">src/contrib/drat_0.0.1.1.tar.gz</span>

<span class="kw">no</span> changes added to commit (use <span class="st">&quot;git add&quot;</span> and/or <span class="st">&quot;git commit -a&quot;</span>)
<span class="kw">edd@max</span>:~/git/drat(gh-pages)$</code></pre>
<p>All is left to is to add, commit and push---either as I usually via the <a href="https://magit.github.io/">spectacularly useful editor mode</a>, or on the command-line, or by simply adding <code>commit=TRUE</code> in the call to <code>insert()</code> or <code>insertPackage()</code>.</p>
<p>I prefer to use <a href="http://dirk.eddelbuettel.com/code/littler.html">littler's r</a> for command-line work, so I am setting the desired repos in <code>~/.littler.r</code> which is read on startup (since <a href="http://dirk.eddelbuettel.com/blog/2015/01/30#littler-0.2.2">the recent littler release 0.2.2</a>) with these two lines:</p>
<pre class="sourceCode r"><code class="sourceCode r">
## add RStudio CRAN mirror
drat:::<span class="kw">add</span>(<span class="st">&quot;CRAN&quot;</span>, <span class="st">&quot;http://cran.rstudio.com&quot;</span>)

## add Dirk&#39;s drat
drat:::<span class="kw">add</span>(<span class="st">&quot;eddelbuettel&quot;</span>)</code></pre>
<p>After that, repos are set as I like them (at home at least):</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ r -e<span class="st">&#39;print(options(&quot;repos&quot;))&#39;</span>
<span class="ot">$repos</span>
                                 <span class="kw">CRAN</span>                          eddelbuettel 
            <span class="st">&quot;http://cran.rstudio.com&quot;</span> <span class="st">&quot;http://eddelbuettel.github.io/drat/&quot;</span> 

<span class="kw">edd@max</span>:~/git$ </code></pre>
<p>And with that, we can just call <code>update.packages()</code> specifying the package directory to update:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ r -e <span class="st">&#39;update.packages(ask=FALSE, lib.loc=&quot;/usr/local/lib/R/site-library&quot;)&#39;</span>                                                                                                                            
<span class="kw">trying</span> URL <span class="st">&#39;http://eddelbuettel.github.io/drat/src/contrib/drat_0.0.1.1.tar.gz&#39;</span>
<span class="kw">Content</span> type <span class="st">&#39;application/octet-stream&#39;</span> length 5829 bytes
<span class="kw">opened</span> URL
==================================================
<span class="kw">downloaded</span> 5829 bytes

<span class="kw">*</span> installing *source* package ‘drat’ ...
<span class="kw">**</span> R
<span class="kw">**</span> inst
<span class="kw">**</span> preparing package for lazy loading
<span class="kw">**</span> help
<span class="kw">***</span> installing help indices
<span class="kw">**</span> building package indices
<span class="kw">**</span> testing if installed package can be loaded
<span class="kw">*</span> DONE (drat)

<span class="kw">The</span> downloaded source packages are in
        ‘<span class="kw">/tmp</span>/<span class="kw">downloaded_packages</span>’
<span class="kw">edd@max</span>:~/git$</code></pre>
<p>and presto, a new version of a package we have installed (here the very <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> interim release we just pushed above) is updated.</p>
<p>Writing this up made me realize I need to update the handy <code>update.r</code> script (see e.g. the <a href="http://dirk.eddelbuettel.com/code/littler.examples.html">littler examples page</a> for more) and it hard-wires just one repo which needs to be relaxed for <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>. Maybe in <code>install2.r</code> which already has <a href="https://github.com/docopt/docopt.R">docopt</a> support...</p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
