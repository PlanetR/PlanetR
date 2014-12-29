---
title: "coneproj: An R Package for the Primal or Dual Cone Projections with Routines for Constrained Regression"
kind: article
created_at: 2014-11-25 08:00:00 UTC
author: Journal of Statistical Software
categories: 
tags: 
layout: post
---
<p>Vol. 61, Issue 12, Nov 2014</p><p>Abstract: <p>The coneproj package contains routines for cone projection and quadratic programming, plus applications in estimation and inference for constrained parametric regression and shape-restricted regression problems. A short routine check_irred is included to check the irreducibility of a matrix, whose rows are supposed to be a set of cone edges used by coneA or coneB. For the coneA and coneB functions, the vector to project is provided by the user, along with the cone specification and a weight vector. For coneA, a constraint matrix is specified to define the cone, and for coneB, the cone edges are provided. The coneA and coneB algorithms have been coded and compiled in C++, and are called by R. The qprog function transforms a quadratic programming problem into a cone projection problem and calls coneA. The constreg function does estimation and inference for parametric least-squares regression with constraints on the parameters (using coneA). A p value for the “one-sided&quot; test is provided. The shapereg function uses coneB to provide a least-squares estimator for a regression function with several choices of constraints including isotonic and convex regression functions, as well as estimates of parametrically modeled covariate effects. Results from hypothesis tests for significance of the effects are also provided. This package is now available from the Comprehensive R Archive Network at http://CRAN.R-project.org/package=coneproj.</p></p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Journal of Statistical Software</a> - check out <a href="http://www.jstatsoft.org/rss">Journal of Statistical Software</a></i>
  </span>
</div>
