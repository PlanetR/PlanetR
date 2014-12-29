---
title: "Introducing RcppParallel: Getting R and C++ to work (some more) in parallel"
kind: article
created_at: 2014-07-16 14:56:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
A common theme over the last few decades was that we could afford to simply
sit back and let computer (hardware) engineers take care of increases in
computing speed thanks to 
<a href="http://en.wikipedia.org/wiki/Moore's_law">Moore's law</a>.
That same line of thought now frequently points out that we
are getting closer and closer to the physical limits of what
<a href="http://en.wikipedia.org/wiki/Moore's_law">Moore's law</a> can
do for us.

<p></p>

So the new best hope is (and has been) parallel processing.  Even our smartphones have
multiple cores, and most if not all retail PCs now possess two, four or more
cores.  Real computers, aka somewhat decent servers, can be had with 24, 32
or more cores as well, and all that is before we even consider GPU
coprocessors or <a href="http://en.wikipedia.org/wiki/Xeon_Phi">other upcoming changes</a>.

<p></p>

And sometimes our tasks are embarassingly simple as is the case with many
data-parallel jobs:  we can use higher-level operations such as those offered
by the base R package <a href="https://stat.ethz.ch/R-manual/R-devel/library/parallel/doc/parallel.pdf">parallel</a> 
to spawn multiple processing tasks and gather the results. I covered all this
in some detail in previous <a href="http://dirk.eddelbuettel.com/presentations.html">talks</a>
on High Performance Computing with R (and you can also consult the
<a href="http://cran.r-project.org/web/views/HighPerformanceComputing.html">Task View on High Performance Computing with R</a>
which I edit).

<p></p>

But sometimes we can't use data-parallel approaches. Hence we have to redo our algorithms. Which is
<em>really hard</em>. R itself has been relying on the (fairly mature) <a href="http://openmp.org/wp/">OpenMP</a>
standard for some of its operations.  Luke Tierney's  
<a href="http://www.rinfinance.com/agenda/2014/talk/LukeTierney.pdf">(awesome) keynote</a> in May at our
(sixth) R/Finance conference mentioned some of the issues related to
<a href="http://openmp.org/wp/">OpenMP</a>.  One which matters
is that <a href="http://openmp.org/wp/">OpenMP</a> works really well on Linux, and
either not so well (Windows) or not at all (OS X, due the usual issue with
the gcc/clang switch enforced by Applem but the good news is that the OpenMP
toolchain is expected to make it to OS X is some more performant form
"soon").   R is still expected to make wider use of OpenMP in future versions.

<p></p>

Another tool which has been around for a few years, and which can be considered
to be equally mature is the
<a href="https://www.threadingbuildingblocks.org/">Intel Threaded Building Blocks</a> 
library, or TBB.  JJ recently started to wrap this up for use by R. The first
approach resulted in a (now superseded, see below) package TBB.
But hardware and OS issues bite once again, as the Intel TBB is not really
building that well for the Windows toolchain used by R (and based on MinGW).

<p></p>
(And yes, there are two more options. But Boost Threads requires linking
which precludes easy use as e.g. via our
<a href="http://cran.rstudio.com/package=BH">BH</a> package. And C++11 with its
threads library (based on Boost Threads) is not yet as widely available as R
and Rcpp which means that it is not a real deployment option yet.)

<p></p>

Now, JJ, being as awesome as he is, went back to the drawing board and integrated a
second threading toolkit: <a href="http://tinythreadpp.bitsnbites.eu/">TinyThread++</a>,
a small header-only library without further dependencies.  Not as
feature-rich as <a href="https://www.threadingbuildingblocks.org/">Intel Threaded Building Blocks</a>, 
but at least available everywhere.  So a new package
<a href="https://github.com/RcppCore/RcppParallel">RcppParallel</a>, so far
only on GitHub, wraps around both <a href="http://tinythreadpp.bitsnbites.eu/">TinyThread++</a> 
and <a href="https://www.threadingbuildingblocks.org/">Intel Threaded Building Blocks</a> and
offers a consistent interface available on all platforms used by R.  

<p></p>

Better still, JJ also authored several pieces demonstrating this new package for the
<a href="http://gallery.rcpp.org">Rcpp Gallery</a>:
<ul>
  <li><a href="http://gallery.rcpp.org/articles/parallel-matrix-transform">A parallel matrix transformation</a></li>
  <li><a href="http://gallery.rcpp.org/articles/parallel-vector-sum">A parallel vector summation</a></li>
  <li><a href="http://gallery.rcpp.org/articles/parallel-inner-product">A parallel inner product</a></li>
  <li><a href="http://gallery.rcpp.org/articles/parallel-distance-matrix">Parallel Distance Matrix Calculation with RcppParallel</a></li>
</ul>

<p></p>

All four are interesting and demonstrate different aspects of parallel
computing via <a href="https://github.com/RcppCore/RcppParallel">RcppParallel</a>.
But the last article is key.  Based on a question by Jim Bullard, and then
written with Jim, it shows how a particular matrix distance metric (which is
missing from R) can be implemented in a serial manner in both R, and
also via Rcpp. The key implementation, however, uses both Rcpp and
<a href="https://github.com/RcppCore/RcppParallel">RcppParallel</a> and
thereby achieves a truly impressive speed gain as the gains from using
compiled code (via Rcpp) and from using a parallel algorithm (via
RcppParallel) are multiplicative!  Between JJ's and my four-core machines the
gain was between 200 and 300 fold---which is rather considerable.  For
kicks, I also used a much bigger machine at work which came in at an even
larger speed gain (but gains become clearly sublinear as the number of cores
increases; there are however some tuning parameters). 

<p></p>

So these are exciting times. I am sure there will be lots more to come.  For
now, head over to the <a href="https://github.com/RcppCore/RcppParallel">RcppParallel</a>
package and start playing. Further contributions to the
<a href="http://gallery.rcpp.org">Rcpp Gallery</a> are not only welcome but
strongly encouraged.<div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
