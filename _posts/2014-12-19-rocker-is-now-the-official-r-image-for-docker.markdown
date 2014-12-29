---
title: "Rocker is now the official R image for Docker"
kind: article
created_at: 2014-12-19 20:51:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p><img alt="big deal" style="float:left;margin:10px 40px 10px 0;" width="300"
     src="http://www.quickmeme.com/img/02/02e43a111301757e9ec260cb458f546ec9f1c32ef8a34adba26fb13011d30cb6.jpg"/></p>
<p>Something happened a little while ago which we did not have time to commensurate properly. Our <a href="http://dirk.eddelbuettel.com/blog/2014/10/23#introducing_rocker">Rocker image for R</a> is now the official R image for Docker itself. So getting R (via Docker) is now as simple as saying <code>docker pull r-base</code>.</p>
<p>This particular container is essentially <em>just</em> the standard <a href="https://tracker.debian.org/pkg/r-base">r-base</a> Debian package for R (which is <a href="https://qa.debian.org/developer.php?email=edd%40debian.org">one of a few I maintain</a> there) plus a mininal set of extras. This <code>r-base</code> forms the basis of our other containers as e.g. the rather popular <code>r-studio</code> container wrapping the excellent <a href="http://www.rstudio.com/products/rstudio">RStudio Server</a>.</p>
<p>A lot of work went into this. <a href="http://www.carlboettiger.info/">Carl</a> and I also got a tremendous amount of help from the good folks at Docker. Details are as always at the <a href="https://github.com/rocker-org/rocker">Rocker repo at GitHub</a>.</p>
<p>Docker itself continues to make great strides, and it has been great fun help to help along. With this post I achieved another goal: blog about Docker with an image <a href="https://twitter.com/solomonstre/status/538813036320923648">not containing shipping containers</a>. Just kidding.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
</p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
