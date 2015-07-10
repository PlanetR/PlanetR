---
title: "Introducing drat: Lightweight R Repositories"
kind: article
created_at: 2015-02-05 14:41:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A new package of mine just got to <a href="http://cran.r-project.org">CRAN</a> in its very first version 0.0.1: <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>. Its name stands for <em>drat R Archive Template</em>, and an introduction is provided at the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> page, the <a href="https://github.com/eddelbuettel/drat">GitHub repository</a>, and below.</p>
<p><a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> builds on a core strength of R: the ability to query multiple repositories. Just how one could always query, say, <a href="http://cran.r-project.org">CRAN</a>, <a href="http://www.bioconductor.org">BioConductor</a> and <a href="http://www.omegahat.org">OmegaHat</a>---one can now adds <em>drats</em> of one or more other developers with ease. <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> also builds on a core strength of <a href="https://github.com">GitHub</a>. Every user automagically has a corresponding <code>github.io</code> address, and by appending <code>drat</code> we are getting a standardized URL.</p>
<p><a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> combines both strengths. So after an initial <code>install.packages(&quot;drat&quot;)</code> to get <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>, you can just do either one of</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(drat)
<span class="kw">addRepo</span>(<span class="st">&quot;eddelbuettel&quot;</span>)</code></pre>
<p>or equally</p>
<pre class="sourceCode r"><code class="sourceCode r">drat:::<span class="kw">add</span>(<span class="st">&quot;eddelbuettel&quot;</span>)</code></pre>
<p>to register my <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>. Now <code>install.packages()</code> will work using this new <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>, as will <code>update.packages()</code>. The fact that the update mechanism works is a key strength: not only can you get a package, but you can gets its updates once its author replaces them into his <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>.</p>
<p>How does one do that? Easy! For a package <code>foo_0.1.0.tar.gz</code> we do</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(drat)
<span class="kw">insertPackage</span>(<span class="st">&quot;foo_0.1.0.tar.gz&quot;</span>)</code></pre>
<p>The default git repository locally is taken as the default <code>~/git/drat/</code> but can be overriden as both a local default (via <code>options()</code>) or directly on the command-line. Note that this also assumes that you a) have a <code>gh-pages</code> branch and b) have that branch as the currently active branch. Automating this / testing for this is left for a subsequent release. Also available is an alternative unexported short-hand function:</p>
<pre class="sourceCode r"><code class="sourceCode r">drat:::<span class="kw">insert</span>(<span class="st">&quot;foo_0.1.0.tar.gz&quot;</span>, <span class="st">&quot;/opt/myWork/git&quot;</span>)</code></pre>
<p>show here with the alternate use case of a local fileshare you can copy into and query from---something we do at work where we share packages only locally.</p>
<p>The easiest way to obtain the corresponding file system layout may be to just fork the <a href="https://github.com/eddelbuettel/drat">drat repository</a>.</p>
<p>So that is it. Two exported functions, and two unexported (potentially name-clobbering) shorthands. Now drat away!</p>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is also a copy of the <code>DESCRIPTION</code> file for <a href="http://dirk.eddelbuettel.com/cranberries/2015/02/05#drat_0.0.1">this initial release</a>. More detailed information is on the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> page.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
