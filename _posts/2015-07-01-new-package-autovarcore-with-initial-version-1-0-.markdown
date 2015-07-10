---
title: "New package autovarCore with initial version 1.0-0 "
kind: article
created_at: 2015-07-01 13:12:00 UTC
author: CRANberries
categories: 
tags: 
layout: post
---
<strong>Package</strong>: autovarCore<br>
<strong>Type</strong>: Package<br>
<strong>Title</strong>: Automated Vector Autoregression Models and Networks<br>
<strong>Version</strong>: 1.0-0<br>
<strong>Date</strong>: 2015-06-29<br>
<strong>Authors@R</strong>: c(person("Ando","Emerencia",role = c("aut","cre"),
email = "ando.emerencia@gmail.com"))<br>
<strong>BugReports</strong>: https://github.com/roqua/autovarcore/issues<br>
<strong>Maintainer</strong>: Ando Emerencia &lt;ando.emerencia@gmail.com&gt;<br>
<strong>Description</strong>: Automatically find the best vector autoregression
models and networks for a given time series data set. 'AutovarCore'
evaluates eight kinds of models: models with and without log
transforming the data, lag 1 and lag 2 models, and models with and
without day dummy variables. For each of these 8 model configurations,
'AutovarCore' evaluates all possible combinations for including
outlier dummies (at 2.5x the standard deviation of the residuals)
and retains the best model. Model evaluation includes the Eigenvalue
stability test and a configurable set of residual tests. These eight
models are further reduced to four models because 'AutovarCore'
determines whether adding day dummies improves the model fit.<br>
<strong>License</strong>: MIT + file LICENSE<br>
<strong>Suggests</strong>: testthat, roxygen2<br>
<strong>Imports</strong>: Rcpp (&gt;= 0.11.4), Amelia, jsonlite, parallel, stats, urca,
vars<br>
<strong>LinkingTo</strong>: Rcpp<br>
<strong>NeedsCompilation</strong>: yes<br>
<strong>Packaged</strong>: 2015-07-01 11:54:26 UTC; ando<br>
<strong>Author</strong>: Ando Emerencia [aut, cre]<br>
<strong>Repository</strong>: CRAN<br>
<strong>Date/Publication</strong>: 2015-07-01 14:41:42<br>

<p>
<a href="http://cran.r-project.org/web/packages/autovarCore/index.html">More information about autovarCore at CRAN</a><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">CRANberries</a> - check out <a href="http://dirk.eddelbuettel.com/cranberries">CRANberries   </a></i>
  </span>
</div>
