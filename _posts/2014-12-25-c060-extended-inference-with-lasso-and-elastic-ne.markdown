---
title: "c060: Extended Inference with Lasso and Elastic-Net Regularized Cox and Generalized Linear Models"
kind: article
created_at: 2014-12-25 08:00:00 UTC
author: Journal of Statistical Software
categories: 
tags: 
layout: post
---
<p>Vol. 62, Issue 5, Dec 2014</p><p>Abstract: <p>We have developed the R package c060 with the aim of improving R software func- tionality for high-dimensional risk prediction modeling, e.g., for prognostic modeling of survival data using high-throughput genomic data. Penalized regression models provide a statistically appealing way of building risk prediction models from high-dimensional data. The popular CRAN package glmnet implements an efficient algorithm for fitting penalized Cox and generalized linear models. However, in practical applications the data analysis will typically not stop at the point where the model has been fitted. One is for example often interested in the stability of selected features and in assessing the prediction performance of a model and we provide functions to deal with both of these tasks. Our R functions are computationally efficient and offer the possibility of speeding up computing time through parallel computing. Another feature which can drastically reduce computing time is an efficient interval-search algorithm, which we have implemented for selecting the optimal parameter combination for elastic net penalties. These functions have been useful in our daily work at the Biostatistics department (C060) of the German Cancer Research Center where prognostic modeling of patient survival data is of particular interest. Although we focus on a survival data application of penalized Cox models in this article, the functions in our R package are in general applicable to all types of regression models implemented in the glmnet package, with the exception of prediction error curves, which are specific to time-to-event data.</p></p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Journal of Statistical Software</a> - check out <a href="http://www.jstatsoft.org/rss">Journal of Statistical Software</a></i>
  </span>
</div>
