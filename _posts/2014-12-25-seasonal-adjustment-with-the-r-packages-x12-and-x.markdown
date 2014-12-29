---
title: "Seasonal Adjustment with the R Packages x12 and x12GUI"
kind: article
created_at: 2014-12-25 08:00:00 UTC
author: Journal of Statistical Software
categories: 
tags: 
layout: post
---
<p>Vol. 62, Issue 2, Dec 2014</p><p>Abstract: <p>The X-12-ARIMA seasonal adjustment program of the US Census Bureau extracts the different components (mainly: seasonal component, trend component, outlier component and irregular component) of a monthly or quarterly time series. It is the state-of-the- art technology for seasonal adjustment used in many statistical offices. It is possible to include a moving holiday effect, a trading day effect and user-defined regressors, and additionally incorporates automatic outlier detection. The procedure makes additive or multiplicative adjustments and creates an output data set containing the adjusted time series and intermediate calculations.
<br />The original output from X-12-ARIMA is somehow static and it is not always an easy task for users to extract the required information for further processing. The R package x12 provides wrapper functions and an abstraction layer for batch processing of X-12-ARIMA. It allows summarizing, modifying and storing the output from X-12-ARIMA within a well-defined class-oriented implementation. On top of the class-oriented (command line) implementation the graphical user interface allows access to the R package x12 without requiring too much R knowledge. Users can interactively select additive outliers, level shifts and temporary changes and see the impact immediately.
<br />The provision of the powerful X-12-ARIMA seasonal adjustment program available directly from within R, as well as of the new facilities for marking outliers, batch processing and change tracking, makes the package a potent and functional tool.</p></p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Journal of Statistical Software</a> - check out <a href="http://www.jstatsoft.org/rss">Journal of Statistical Software</a></i>
  </span>
</div>
