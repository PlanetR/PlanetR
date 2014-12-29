---
title: "Introducing pkgKitten:  Creating R Packages that purr"
kind: article
created_at: 2014-06-13 14:58:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
A new package <a href="http://dirk.eddelbuettel.com/code/pkgkitten.html"><strong>pkgKitten</strong></a> 
is now on CRAN in its infant version 0.1.0.

<p></p>
It does only one thing: create R packages that do not suck.  Or at least not
as much as those created by the (R default) function <code>package.skeleton()</code> which
creates files which the very standard, and very recommended, <code>R CMD check</code> then complains
about.  That is silly. Because each time <code>R CMD check</code> complains,
something bad happens to a kitten somewhere. 

<p></p>
So <a href="http://dirk.eddelbuettel.com/code/pkgkitten.html">pkgKitten</a> offers
a wrapper function <code>kitten()</code> which creates neat little packages
which do not upset <code>R CMD check</code>.

<p></p>
A complete little demo is on the 
<a href="http://dirk.eddelbuettel.com/code/pkgkitten.html">pkgKitten webpage</a>
which also has pointers to the
<a href="https://github.com/eddelbuettel/pkgkitten">pkgKitten GitHub repo</a>.


<p></p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a>
originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog.
Please report excessive re-aggregation in third-party for-profit settings. 
<p></p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
