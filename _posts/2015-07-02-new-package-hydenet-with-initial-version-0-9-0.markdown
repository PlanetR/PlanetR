---
title: "New package HydeNet with initial version 0.9.0 "
kind: article
created_at: 2015-07-02 23:13:00 UTC
author: CRANberries
categories: 
tags: 
layout: post
---
<strong>Package</strong>: HydeNet<br>
<strong>Type</strong>: Package<br>
<strong>Title</strong>: Hybrid Bayesian Networks Using R and JAGS<br>
<strong>Version</strong>: 0.9.0<br>
<strong>Date</strong>: 2015-07-2<br>
<strong>Author</strong>: Jarrod E. Dalton &lt;daltonj@ccf.org&gt; and Benjamin Nutter &lt;benjamin.nutter@gmail.com&gt;<br>
<strong>Maintainer</strong>: Benjamin Nutter &lt;benjamin.nutter@gmail.com&gt;<br>
<strong>Description</strong>: Facilities for easy implementation of hybrid Bayesian networks
using R. Bayesian networks are directed acyclic graphs representing joint
probability distributions, where each node represents a random variable and
each edge represents conditionality. The full joint distribution is
therefore factorized as a product of conditional densities, where each node
is assumed to be independent of its non-descendents given information on its
parent nodes. Since exact, closed-form algorithms are computationally
burdensome for inference within hybrid networks that contain a combination
of continuous and discrete nodes, particle-based approximation techniques
like Markov Chain Monte Carlo are popular.  We provide a user-friendly
interface to constructing these networks and running inference using the 'rjags' package.
Econometric analyses (maximum expected utility under competing policies,
value of information) involving decision and utility nodes are also
supported.<br>
<strong>License</strong>: MIT + file LICENSE<br>
<strong>Depends</strong>: R (&gt;= 3.0.0), nnet, rjags<br>
<strong>Imports</strong>: broom (&gt;= 0.3.7), DiagrammeR (&gt;= 0.7), plyr, dplyr, graph,
gRbase, magrittr, stats, stringr, utils<br>
<strong>Suggests</strong>: knitr<br>
<strong>SystemRequirements</strong>: JAGS (http://mcmc-jags.sourceforge.net)<br>
<strong>VignetteBuilder</strong>: knitr<br>
<strong>LazyLoad</strong>: yes<br>
<strong>LazyData</strong>: true<br>
<strong>URL</strong>: https://github.com/nutterb/HydeNet,<br>
<strong>BugReports</strong>: https://github.com/nutterb/HydeNet/issues<br>
<strong>NeedsCompilation</strong>: no<br>
<strong>Packaged</strong>: 2015-07-02 18:11:38 UTC; Nutter<br>
<strong>Repository</strong>: CRAN<br>
<strong>Date/Publication</strong>: 2015-07-03 00:31:59<br>

<p>
<a href="http://cran.r-project.org/web/packages/HydeNet/index.html">More information about HydeNet at CRAN</a><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">CRANberries</a> - check out <a href="http://dirk.eddelbuettel.com/cranberries">CRANberries   </a></i>
  </span>
</div>
