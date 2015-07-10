---
title: "drat 0.0.4: Yet more features and documentation"
kind: article
created_at: 2015-05-27 12:06:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A new version, now at 0.0.4, of the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> package arrived on <a href="http://cran.r-project.org">CRAN</a> yesterday. Its name stands for <em>drat R Archive Template</em>, and it helps with easy-to-create and easy-to-use <em>repositories</em> for R packages, and is finding increasing by other projects.</p>
<p>Version 0.0.4 brings both new code and more documentation:</p>
<ul>
<li>support for binary repos on Windows and OS X thanks to <a href="http://www.katzien.de/">Jan Schulz</a>;</li>
<li>new (still raw) helper functions <code>initRepo()</code> to create a git-based repository, and <code>pruneRepo()</code> to remove older versions of packages;</li>
<li>the <code>insertRepo()</code> functions now uses <code>tryCatch()</code> around git commands (with thanks to <a href="http://www.carlboettiger.info/">Carl Boettiger</a>);</li>
<li>when adding a file to a <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> repo we ensure that the repo path does not contains spaces (with thank to <a href="http://www.stefanbache.dk/">Stefan Bache</a>);</li>
<li>stress that file-based repos need a URL of the form <code>file:/some/path</code> with one colon but not two slashes (also thanks to <a href="http://www.stefanbache.dk/">Stefan Bache</a>);</li>
<li>new <a href="http://eddelbuettel.github.io/drat/CombiningDratAndTravis.html">Using Drat with Travis CI</a> vignette thanks to <a href="http://www.mas.ncl.ac.uk/~ncsg3/">Colin Gillespie</a>;</li>
<li>new <a href="http://eddelbuettel.github.io/drat/DratFAQ.html">Drat FAQ</a> vignette;</li>
<li>other fixes and extensions.</li>
</ul>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is a comparison to <a href="http://dirk.eddelbuettel.com/cranberries/2015/05/26#drat_0.0.4">the previous release</a>. More detailed information is on the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> page.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
