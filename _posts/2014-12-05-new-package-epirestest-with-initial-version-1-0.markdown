---
title: "New package EpiResTest with initial version 1.0 "
kind: article
created_at: 2014-12-05 15:12:00 UTC
author: CRANberries
categories: 
tags: 
layout: post
---
<strong>Package</strong>: EpiResTest<br>
<strong>Type</strong>: Package<br>
<strong>Title</strong>: Latent Residuals Test for Epidemiology and Ecology Models<br>
<strong>Version</strong>: 1.0<br>
<strong>Date</strong>: 2014-07-07<br>
<strong>Author</strong>: Max S. Y. Lau; Jeffrey Pollock<br>
<strong>Maintainer</strong>: Max S. Y. Lau <maxlauhk54@gmail.com><br>
<strong>Description</strong>: Latent residual tests recently developed (Lau et al. 2014) which
are specifically designed to measure the goodness-of-fit of different model
components of a general spatial S-E-I-R model commonly used in epidemiology
and ecology studies. More restrictive model classes such as S-I-R can be
accommodated. Note that although each test is specifically designed to be
sensitive to one particular component of a spatio-temporal model, they are
not theoretically restricted to only testing these specific aspects and can
be used as a general model assessment tool like any other conventional
model selection techniques. The underlying functions are coded in C++ so
they should be generally quick.<br>
<strong>Note</strong>: Under the null hypothesis that the model is correct, the
residuals follow distribution U(0,1). The examples only compute
a single set of residuals given actual values of most of the
model components which are typically required to be imputed in
data augmentation schemes such as MCMC in which multiple sets
of residuals can be imputed. Only the raw residuals are
outputted, a natural summary statistics of the residual samples
is the p-value which may be computed using Kolmogorov-Smirnov
or Anderson-Darling test.<br>
<strong>License</strong>: GPL (>= 2)<br>
<strong>Imports</strong>: Rcpp (>= 0.11.2)<br>
<strong>LinkingTo</strong>: Rcpp, RcppArmadillo<br>
<strong>Suggests</strong>: RUnit, ADGofTest<br>
<strong>Packaged</strong>: 2014-12-05 14:12:57 UTC; sl451<br>
<strong>NeedsCompilation</strong>: yes<br>
<strong>Repository</strong>: CRAN<br>
<strong>Date/Publication</strong>: 2014-12-05 15:29:39<br>

<p>
<a href="http://cran.r-project.org/web/packages/EpiResTest/index.html">More information about EpiResTest at CRAN</a><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">CRANberries</a> - check out <a href="http://dirk.eddelbuettel.com/cranberries">CRANberries   </a></i>
  </span>
</div>
