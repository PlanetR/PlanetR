---
title: "&lt;h2 id=&quot;introducing-rocker-docker-for-r&quot;&gt;Introducing Rocker: Docker for R&lt;/h2&gt;"
kind: article
created_at: 2014-10-23 16:39:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<blockquote>
<p>You only know two things about Docker. First, it uses Linux<br />containers. Second, the Internet won't shut up about it.</p>
<p>-- attributed to Solomon Hykes, Docker CEO</p>
</blockquote>
<h3 id="so-what-is-docker">So what is Docker?</h3>
<p><a href="http://www.docker.com">Docker</a> is a relatively new <a href="https://github.com/docker/docker/tree/master/LICENSE">open source</a> application and service, which is seeing interest across a number of areas. It uses recent Linux kernel features (containers, namespaces) to shield processes. While its use (superficially) resembles that of virtual machines, it is <em>much more lightweight</em> as it operates at the level of a single process (rather than an emulation of an entire OS layer). This also allows it to start almost instantly, require very little resources and hence permits an order of magnitude more deployments per host than a virtual machine.</p>
<p><a href="http://www.docker.com">Docker</a> offers a standard interface to creation, distribution and deployment. The <em>shipping container</em> analogy is apt: just how shipping containers (via their standard size and &quot;interface&quot;) allow global trade to prosper, Docker is aiming for nothing less for deployment. A <a href="https://docs.docker.com/articles/dockerfile_best-practices/">Dockerfile</a> provides a concise, extensible, and executable description of the computational environment. Docker software then builds a <a href="https://docs.docker.com/userguide/dockerimages/">Docker image</a> from the Dockerfile. Docker images are analogous to virtual machine images, but smaller and built in discrete, extensible and reuseable layers. Images can be distributed and run on any machine that has Docker software installed---including Windows, OS X and of course Linux. Running instances are called <a href="https://docs.docker.com/userguide/usingdocker/">Docker containers</a>. A single machine can run hundreds of such containers, including multiple containers running the same image.</p>
<p>There are many good tutorials and introductory materials on <a href="http://www.docker.com">Docker</a> on the web. The <a href="https://www.docker.com/tryit/">official online tutorial</a> is a good place to start; this post can not go into more detail in order to remain short and introductory.</p>
<h3 id="so-what-is-rocker">So what is Rocker?</h3>
<p><img alt="rocker logo"
     style="float:left;margin:10px 40px 10px 0;"
     width="100" height="100"
     src="https://en.gravatar.com/userimage/73204427/563567819bd642c7a9e3af9d8ddb7581.png?size=100"/></p>
<p>At its core, Rocker is a project for running <a href="http://www.r-project.org">R</a> using Docker containers. We provide a collection of Dockerfiles and pre-built Docker images that can be used and extended for many purposes.</p>
<p><a href="https://github.com/rocker-org/rocker">Rocker</a> is the the name of our <a href="https://github.com/">GitHub</a> repository contained with the <a href="https://github.com/rocker-org">Rocker-Org</a> GitHub organization.</p>
<p><a href="https://hub.docker.com/account/organizations/rocker/">Rocker</a> is also the name the account under which the automated builds at <a href="http://www.docker.com">Docker</a> provide containers ready for download.</p>
<h3 id="current-rocker-status">Current Rocker Status</h3>
<h4 id="core-rocker-containers">Core Rocker Containers</h4>
<p>The Rocker project develops the following containers in the core Rocker repository</p>
<ul>
<li><a href="https://registry.hub.docker.com/u/rocker/r-base/">r-base</a> provides a base R container to build from</li>
<li><a href="https://registry.hub.docker.com/u/rocker/r-devel/">r-devel</a> provides the basic R container, as well as a complete R-devel build based on current SVN sources of R</li>
<li><a href="https://registry.hub.docker.com/u/rocker/rstudio/">rstudio</a> provides the base R container as well an <a href="http://www.rstudio.com/products/rstudio/">RStudio Server</a> instance</li>
</ul>
<p>We have settled on these three core images after earlier work in repositories such as docker-debian-r and docker-ubuntu-r.</p>
<h4 id="rocker-use-case-containers">Rocker Use Case Containers</h4>
<p>Within the Rocker-org organization on GitHub, we are also working on</p>
<ul>
<li><a href="https://registry.hub.docker.com/u/rocker/hadleyverse/">Hadleyverse</a> which extends the rstudio container with a number of Hadley packages</li>
<li><a href="https://registry.hub.docker.com/u/rocker/ropensci/">rOpenSci</a> which extends hadleyverse with a number of <a href="http://ropensci.org/">rOpenSci</a> packages</li>
<li><a href="https://registry.hub.docker.com/u/rocker/r-devel-san/">r-devel-san</a> provides an R-devel build for &quot;Sanitizer&quot; run-time diagnostics via a properly instrumented version of R-devel via a recent compiler build</li>
<li><a href="https://github.com/rocker-org/rocker-versioned">rocker-versioned</a> aims to provided containers with 'versioned' previous R releases and matching packages</li>
</ul>
<p>Other repositories will probably be added as new needs and opportunities are identified.</p>
<h3 id="deprecation">Deprecation</h3>
<p>The Rocker effort supersedes and replaces earlier work by Dirk (in the docker-debian-r and docker-ubuntu-r GitHub repositories) and Carl. Please use the <a href="https://github.com/rocker-org/rocker">Rocker GitHub repo</a> and <a href="https://hub.docker.com/account/organizations/rocker/">Rocker Containers from Docker.com</a> going forward.</p>
<h3 id="next-steps">Next Steps</h3>
<p>We intend to follow-up with more posts detailing usage of both the source Dockerfiles and binary containers on different platforms.</p>
<p>Rocker containers are fully functional. We invite you to take them for a spin. Bug reports, comments, and suggestions are welcome; we suggest you use the <a href="https://github.com/rocker-org/rocker/issues">GitHub issue tracker</a>.</p>
<h3 id="acknowledgments">Acknowledgments</h3>
<p>We are very appreciative of all comments received by early adopters and testers. We also would like to thank RStudio for allowing us the redistribution of their RStudio Server binary.</p>
<p>Published concurrently at <a href="http://ropensci.org/blog/">rOpenSci blog</a> and <a href="http://dirk.eddelbuettel.com/blog">Dirk's blog</a>.</p>
<h3 id="authors">Authors</h3>
<p><a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> and <a href="http://www.carlboettiger.info/">Carl Boettiger</a></p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
</p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
