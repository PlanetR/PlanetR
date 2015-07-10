---
title: "drat 0.0.3: More features, more fixes, more documentation"
kind: article
created_at: 2015-04-10 12:14:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>Several weeks ago we introduced the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> package. Its name stands for <em>drat R Archive Template</em>, and it helps with easy-to-create and easy-to-use <em>repositories</em> for R packages. Two early blog posts describe drat: <a href="http://dirk.eddelbuettel.com/blog/2015/02/07#drat_first_steps">First Steps Towards Lightweight Repositories</a>, and <a href="http://dirk.eddelbuettel.com/blog/2015/02/22#drat_second_tutorial_publishing">Publishing a Package</a>, and since the previous release, a <a href="http://dirk.eddelbuettel.com/blog/2015/03/13#drat_guest_post_why_drat">a guest post on drat</a> was also added to the blog.</p>
<p>Several people have started to use drat to publish their packages, and this is a very encouraging sign. I also created a new repository and may have more to say about this in another post once I get time to write something up.</p>
<p>Today version 0.0.3 arrived on <a href="http://cran.r-project.org">CRAN</a>. It rounds out functionality, adds some fixes and brings more documentation:</p>
<ul>
<li>git support via <a href="http://cran.rstudio.com/web/packages/git2r/index.html">git2r</a> is improved; it is still optional (ie <code>commit=TRUE</code> is needed when adding packages) but plan to expand it</li>
<li>several small bugs got fixed, including issues <a href="https://github.com/eddelbuettel/drat/issues/9">#9</a> and <a href="https://github.com/eddelbuettel/drat/issues/7">#7</a>,</li>
<li>four new vignettes got added, including two guests posts by <a href="https://github.com/shabbychef">Steven</a> and <a href="https://github.com/csgillespie">Colin</a> as well as two focusing, respectively, on <a href="http://cran.r-project.org/web/packages/drat/vignettes/DratForPackageAuthors.html">drat for authors</a> and and <a href="http://cran.r-project.org/web/packages/drat/vignettes/DratForPackageUsers.html">drat for users</a>.</li>
</ul>
<p>The work on the vignettes is clearly in progress as Colin's guest post isn't really finished yet, and I am not too impressed with how the markdown is rendered at CRAN so some may still become pdf files instead.</p>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is a comparison to <a href="http://dirk.eddelbuettel.com/cranberries/2015/04/10#drat_0.0.3">the previous release</a>. More detailed information is on the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> page.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
