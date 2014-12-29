---
title: "RPushbullet 0.1.0 with a lot more awesome"
kind: article
created_at: 2014-10-11 03:29:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A new release 0.1.0 of the <a href="http://dirk.eddelbuettel.com/code/rpushbullet.html">RPushbullet</a> package (interfacing the neat <a href="http://www.pushbullet.com">Pushbullet</a> service) landed on <a href="http://cran.r-project.org">CRAN</a> today.</p>
<p>It brings a number of goodies relative to the first release 0.0.2 of a few months ago:</p>
<ul>
<li>pushing of files is now supported thanks to a nice pull request bu Mike Birdgeneau</li>
<li>a default device can be designated in the <code>~/.rpushbullet.json</code> file or options</li>
<li>initialization has been rewritten to use <code>recpients</code> which can be indices, device names or, if missing entirely, the (new) default device</li>
<li>alternatively, <code>email</code> is supported as another recipient option in which case the Pushbullet service will send an email to the give address</li>
<li><code>pbGetDevices()</code> now returns a proper S3 object with corresponding <code>print()</code> and <code>summary()</code> methods</li>
<li>the documentation regarding package initialization, and setting of key, devices, etc has been expanded</li>
<li>more examples has been added to the documentation</li>
<li>various minor cleanups, fixes, corrections throughout</li>
</ul>
<p>There is a whole boat load of more wickedness in the <a href="https://docs.pushbullet.com">Pushbullet API</a> so if anybody feels compelled to add it, fire off <a href="https://github.com/eddelbuettel/rpushbullet">pull requests at GitHub</a>.</p>
<p>More details about the package are at the <a href="http://dirk.eddelbuettel.com/code/rpushbullet.html">RPushbullet webpage</a> and the <a href="https://github.com/eddelbuettel/rpushbullet">RPushbullet GitHub repo</a>.</p>
<p>Courtesy of <a href="http://dirk.eddelbuettel.com/cranberries/">CRANberries</a>, there is also a diffstat report for <a href="http://dirk.eddelbuettel.com/cranberries/2014/10/10#RPushbullet_0.1.0">this release</a>.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
</p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
