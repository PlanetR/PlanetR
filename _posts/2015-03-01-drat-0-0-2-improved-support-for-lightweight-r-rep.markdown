---
title: "drat 0.0.2: Improved Support for Lightweight R Repositories"
kind: article
created_at: 2015-03-01 15:39:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A few weeks ago we introduced the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> package. Its name stands for <em>drat R Archive Template</em>, and it helps with easy-to-create and easy-to-use <em>repositories</em> for R packages. Two early blog posts describe <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>: <a href="http://dirk.eddelbuettel.com/blog/2015/02/07#drat_first_steps">First Steps Towards Lightweight Repositories</a>, and <a href="http://dirk.eddelbuettel.com/blog/2015/02/22#drat_second_tutorial_publishing">Publishing a Package</a>.</p>
<p>A new version 0.0.2 is now on <a href="http://cran.r-project.org">CRAN</a>. It adds several new features:</p>
<ul>
<li>beginnings of native git support via the excellent new <a href="http://cran.r-project.org/web/packages/git2r/index.html">git2r</a> package,</li>
<li>a new helper function to prune a repo of older versions of packages (as R repositories only show the newest release of a package),</li>
<li>improved core functionality in inserting a package, and adding a repo.</li>
</ul>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is a comparison to <a href="http://dirk.eddelbuettel.com/cranberries/2015/03/01#drat_0.0.2">the previous release</a>. More detailed information is on the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> page.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
