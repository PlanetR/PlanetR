---
title: "pkgKitten 0.1.1: Still creating R Packages that purr"
kind: article
created_at: 2014-09-11 01:12:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A maintenance release 0.1.1 of <a href="http://dirk.eddelbuettel.com/code/pkgkitten.html">pkgKitten</a> is now on <a href="http://cran.r-project.org">CRAN</a>.</p>
<p>It has only one small change: the function <code>playWithPerPackageHelpPage()</code> was factored out of the main function <code>kitten()</code> as I happened to be needing something just like <code>playWithPerPackageHelpPage()</code> to make packages created by the <a href="http://dirk.eddelbuettel.com/code/rcpp.html">Rcpp</a> function <code>Rcpp.package.skeleton()</code> a little nicer.</p>
<p>We also added a <code>NEWS.Rd</code> file which restates major release features. As it is so short, we include it in its entirety.</p>
<blockquote>
<h4>
Changes in version 0.1.1 (2014-09-09)
</h4>
<ul>
    <li><p> 
New (exported) function <code>playWithPerPackageHelpPage()</code> which lets other packages create a non-complaint-generating package help page
</p> </li>
</ul>
 

<h4>
Changes in version 0.1.0 (2014-06-13)
</h4>
<ul>
    <li><p> 
Initial public version and CRAN upload
</p> </li>
</ul>
</blockquote>


<p>More details about the package are at the <a href="http://dirk.eddelbuettel.com/code/pkgkitten.html">pkgKitten webpage</a> and the <a href="https://github.com/eddelbuettel/pkgkitten">pkgKitten GitHub repo</a>.</p>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is also a diffstat report for <a href="http://dirk.eddelbuettel.com/cranberries/2014/09/10#pkgKitten_0.1.1">this release</a></p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p></p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
