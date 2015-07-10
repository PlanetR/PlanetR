---
title: "&lt;h3 id=&quot;introducing-ghrr-github-hosted-r-repository&quot;&gt;Introducing ghrr: GitHub Hosted R Repository&lt;/h3&gt;"
kind: article
created_at: 2015-04-21 14:34:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p><img alt="ghrr logo"
     style="float:left;margin:10px 40px 10px 0;" width="250"
     src="https://avatars3.githubusercontent.com/u/11597821?v=3&amp;s=250"/></p>
<h4 id="background">Background</h4>
<p>R relies on package repositories for initial installation of a package via <code>install.packages()</code>. A crucial second step is <code>update.packages()</code>: For all currently installed packages, a list of available updates is constructed or offered for either one-by-one or bulk updates. This keeps the local packages in sync with upstream, and provides for a very convenient way to obtain new features, bug fixes and other improvements. So by installing from a repository, we automatically have the ability to track the repository for updates.</p>
<h4 id="enter-drat">Enter drat</h4>
<p>Fairly recently, the <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> package was added to the R ecosystem. It makes both aspects of package distribution easy: <em>providing</em> a package (if you are an author) as well as <em>installing</em> it (if you are a user). Now, because <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> is at the same time source code (as it is also a package providing the functionality), and a repository (using what <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> provides ib features), the &quot;namespace&quot; becomes a little cluttered.</p>
<p>But because a key feature of <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> is the &quot;one variable&quot; unique identification via the GitHub, I opted to create a drat repository in the name of a new organisation: <a href="http://ghrr.github.io/drat">ghrr</a>. This is a simple acronym for <em>GitHub Hosted R Repository</em>.</p>
<h4 id="use-cases">Use cases</h4>
<p>We can outline several use case for packages in <a href="http://ghrr.github.io/drat">ghrr</a>:</p>
<ul>
<li><em>packages not published in a repo by their authors</em>: I already use two like that:
<ul>
<li><a href="http://rforge.net/fasttime">fasttime</a>, an impeccably fast parser for ISO datetimes by Simon Urbanek which was however never released into a repo by Simon, and</li>
<li><a href="https://github.com/richfitz/RcppR6">RcppR6</a>, a very nice extension to both R6 (by Winston) and Rcpp, by Rich FitzJohn; similarly <em>never released</em> beyond GitHub;</li>
</ul></li>
<li><em>packages possibly unsuitable for mainline repos</em>:
<ul>
<li><a href="https://github.com/armstrtw/Rblpapi">Rblpapi</a> is a great package by Whit Armstong and John Laing to which I have been contributing quite a bit of late. As it requires a free-to-use but not open source library and headers from Bloomberg, it will never make it to the mainline repository for R, but hosting it in <a href="http://ghrr.github.io/drat">ghrr</a> is perfect as I can easily update several machines at work once I cut a new development release;</li>
<li><a href="https://github.com/eddelbuettel/winsorize">winsorize</a> is a small package I needed a few weeks ago; it is spun out of <a href="http://cran.rstudio.com/package=robustHD">robustHD</a> but does not yet contain new code so Andreas and I are content to keep it in this drat for now;</li>
</ul></li>
<li><em>packages in pre-relase mode</em>:
<ul>
<li><a href="http://dirk.eddelbuettel.com/code/rcpp.armadillo.html">RcppArmadillo</a> where I announced both a release candidate before Armadillo 5.000 came out, as well as the actual RcppArmadillo 0.500.0.0 which is not (yet) on the mainline repository as two affected packages need a small update first. Users, however, can get RcppArmadillo already from the sibling <a href="http://RcppCore.github.io/drat">Rcpp drat</a> repo.</li>
<li><a href="https://github.com/eddelbuettel/rcpptoml">RcppToml</a> is a new package I am currently working on implementing a <a href="https://github.com/toml-lang/toml">toml</a> parser based on <a href="https://github.com/skystrife/cpptoml">cpptoml</a>. It works, but it not quite ready for public announcements yet, and hence perfect for <a href="http://ghrr.github.io/drat">ghrr</a>.</li>
</ul></li>
</ul>
<h4 id="going-forward">Going forward</h4>
<p><a href="http://ghrr.github.io/drat">ghrr</a> is meant to be open. While anybody can open a drat repository, particularly on GitHub, it may be beneficial to somehow group packages. This is however not something that can be planned <em>ex-ante</em>: it may just happen if others who see similar benefits in this can in fact contribute. In that spirit, I strongly encourage pull requests.</p>
<p>Early on, I made my commit messages conform to a pattern of <code>package version sha1 repourl</code> to make code provenance of every commit very clear. Ideally, subsequent commits would conform to such a scheme, or replace it with a better one.</p>
<h4 id="some-resources">Some Resources</h4>
<p>A few links to learn more about drat and ghrr:</p>
<ul>
<li><a href="https://github.com/ghrr/drat">ghrr repo view</a> (to see both content and commits) and <a href="http://ghrr.github.io/drat">ghrr web page</a></li>
<li><a href="https://github.com/eddelbuettel/drat">drat repo view</a>, <a href="http://dirk.eddelbuettel.com/code/drat.html">drat code page</a>, and <a href="http://eddelbuettel.github.io/drat">drat web page</a></li>
</ul>
<p>Comments and questions via email or issue tickets are more than welcome. We hope that others find <a href="http://ghrr.github.io/drat">ghrr</a> to be a useful tool for easy repository management and use via GitHub.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
