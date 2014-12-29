---
title: "Introducing RcppRedis"
kind: article
created_at: 2014-06-10 00:46:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<a href="http://dirk.eddelbuettel.com/code/rcppredis.html">RcppRedis</a>,
another new package of mine, appeared on
<a href="http://cran.r-project.org">CRAN</a> a few weeks ago just in time for our
annual <a href="http://www.RinFinance.com">R/Finance</a> conference.

<p></p>
And as of today, we also have Windows binaries thanks to generous help from
John Buonagurio who help building the required 32- and 64-bit libraries for
Windows, and Uwe Ligges who now installed them for the
<a href="http://cran.r-project.org">CRAN</a> and
<a href="http://win-builder.r-project.org">win-builder</a>
machiness. Binaries for release 0.1.1 should be available within a day.

<p></p>
To describe the package, I also just set up a page about
<a href="http://dirk.eddelbuettel.com/code/rcppredis.html">RcppRedis</a>
so rather than repeating everything here I invite you to follow the link.

<p></p>

The ever-so-brief NEWS entry for the two first uploads follows.

<blockquote>
<h4>Changes in version 0.1.1 (2014-06-09)</h4>
<ul>
  <li><p> Now with Windows support thanks to the installation of builds of the hiredis library (created by John Buonagurio) at CRAN / win-builder (thanks to Uwe Ligges) </p> </li>
  <li><p> Added support for new command <code>zcount</code> </p> </li>
</ul>
 
<h4>Changes in version 0.1.0 (2014-05-10)</h4>
<ul>
  <li><p> Initial CRAN upload </p> </li>
</ul>
</blockquote>

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
