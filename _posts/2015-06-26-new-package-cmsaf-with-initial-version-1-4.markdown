---
title: "New package cmsaf with initial version 1.4 "
kind: article
created_at: 2015-06-26 13:13:00 UTC
author: CRANberries
categories: 
tags: 
layout: post
---
<strong>Package</strong>: cmsaf<br>
<strong>Version</strong>: 1.4<br>
<strong>Date</strong>: 2015-06-24<br>
<strong>Title</strong>: Tools for CM SAF netcdf data<br>
<strong>Author</strong>: Steffen Kothe<br>
<strong>Maintainer</strong>: Steffen Kothe &lt;Steffen.Kothe@dwd.de&gt;<br>
<strong>Description</strong>: The Satellite Application Facility on Climate Monitoring (CM SAF)
is a ground segment of the European Organization for the Exploitation of
Meteorological Satellites (EUMETSAT) and one of EUMETSATs Satellite Application
Facilities. The CM SAF contributes to the sustainable observing of the climate
system by providing Essential Climate Variables related to the energy and water
cycle of the atmosphere (www.cmsaf.eu). It is a joint cooperation of seven
National Meteorological and Hydrological Services, including the Deutscher
Wetterdienst (DWD).
The cmsaf R-package provides a small collection of R-functions, which are
inspired by the Climate Data Operators (cdo). This gives the opportunity to
analyse and manipulate CM SAF data without the need of installing cdo.
The cmsaf R-package is tested for CM SAF netcdf data, which are structured
in three-dimensional arrays (longitude, latitude, time) on a rectangular grid.
Layered CM SAF data have to be converted with the provided `levbox_mergetime`
function. The cmsaf R-package functions have only minor checks for deviations
from the recommended data structure, and give only few specific error messages.
Thus, there is no warranty of accurate results.<br>
<strong>License</strong>: GPL (&gt;= 3)<br>
<strong>Depends</strong>: ncdf4, RNetCDF, sp, raster, stats, fields<br>
<strong>Packaged</strong>: 2015-06-26 11:10:52 UTC; stkothe<br>
<strong>NeedsCompilation</strong>: no<br>
<strong>Repository</strong>: CRAN<br>
<strong>Date/Publication</strong>: 2015-06-26 14:00:33<br>

<p>
<a href="http://cran.r-project.org/web/packages/cmsaf/index.html">More information about cmsaf at CRAN</a><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">CRANberries</a> - check out <a href="http://dirk.eddelbuettel.com/cranberries">CRANberries   </a></i>
  </span>
</div>
