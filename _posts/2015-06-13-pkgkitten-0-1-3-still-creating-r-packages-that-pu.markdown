---
title: "pkgKitten 0.1.3: Still creating R Packages that purr"
kind: article
created_at: 2015-06-13 14:13:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A new release, now at version 0.1.3, of <a href="http://dirk.eddelbuettel.com/code/pkgkitten.html">pkgKitten</a> arrived on <a href="http://cran.r-project.org">CRAN</a> this morning.</p>
<p>The main change is (optional) support of the excellent <a href="http://cran.rstudio.com/package=whoami">whoami</a> package by Gabor which allows us to fill in the <code>Author:</code> and <code>Maintainer:</code> fields of the <code>DESCRIPTION</code> file with automatically discovered values. This is however only a <code>Suggests:</code> and not a <code>Depends:</code> to not force the added dependencies on everywhere. We also alter the default values of <code>Title:</code> and <code>Description:</code> so that they actually pass the current level of tests enforced by <code>R CMD check --as-cran</code>.</p>
<blockquote>
<h4>
Changes in version 0.1.3 (2015-06-12)
</h4>
<ul>
<li><p> 
The fields Title: and Description: in the file <code>DESCRIPTION</code> file are now updated such that they actually pass <code>R CMD check</code> on current versions of R.
</p> </li>
<li><p> 
If installed, the <a href="http://cran.rstudio.com/package=whoami">whoami</a> package (version 1.1.0 or later) is now used to discover the username and email in the <code>DESCRIPTION</code> file.
</p> </li>
</ul>
</blockquote>


<p>More details about the package are at the <a href="http://dirk.eddelbuettel.com/code/pkgkitten.html">pkgKitten webpage</a> and the <a href="https://github.com/eddelbuettel/pkgkitten">pkgKitten GitHub repo</a>.</p>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is also a diffstat report for <a href="http://dirk.eddelbuettel.com/cranberries/2015/06/13#pkgKitten_0.1.3">this release</a></p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p></p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
