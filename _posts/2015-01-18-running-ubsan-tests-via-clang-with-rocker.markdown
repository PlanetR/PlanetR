---
title: "Running UBSAN tests via clang with Rocker"
kind: article
created_at: 2015-01-18 20:12:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>Every now and then we get reports from <a href="http://cran.r-project.org">CRAN</a> about our packages failing a test there. A challenging one concerns UBSAN, or <em>Undefined Behaviour Sanitizer</em>. For background on UBSAN, see <a href="http://developerblog.redhat.com/2014/10/16/gcc-undefined-behavior-sanitizer-ubsan/">this RedHat blog post for gcc</a> and <a href="http://blog.llvm.org/2013/04/testing-libc-with-fsanitizeundefined.html">this one from LLVM about clang</a>.</p>
<p>I had written briefly about this before in a <a href="http://dirk.eddelbuettel.com/blog/2014/08/03#sanitizers_0.1.0">blog post introducing the sanitizers package for tests</a>, as well as the <a href="http://dirk.eddelbuettel.com/code/sanitizers.html">corresponding package page for sanitizers</a>, which clearly predates our follow-up <a href="https://github.com/rocker-org">Rocker.org</a> repo / project described <a href="http://dirk.eddelbuettel.com/blog/2014/10/23#introducing_rocker">in this initial announcement</a> and <a href="http://dirk.eddelbuettel.com/blog/2014/12/19#rocker_official_r_image">when we became the official R container for Docker</a>.</p>
<p>Rocker had support for SAN testing, but UBSAN was not working yet. So following a recent CRAN report against our <a href="http://dirk.eddelbuettel.com/code/rcpp.annoy.html">RcppAnnoy</a> package, I was unable to replicate the error and <a href="http://thread.gmane.org/gmane.comp.lang.r.devel/37338">asked for help on r-devel in this thread</a>.</p>
<p>Martyn Plummer and Jan van der Laan kindly sent their configurations in the same thread and off-list; Jeff Horner did so too following an <a href="https://twitter.com/jeffreyhorner/status/555860079241859072">initial tweet offering help</a>. None of these worked for me, but further trials eventually lead me to the (already mentioned above) <a href="http://developerblog.redhat.com/2014/10/16/gcc-undefined-behavior-sanitizer-ubsan/">RedHat blog post</a> with its mention of <code>-fno-sanitize-recover</code> to actually have an error abort a test. Which, coupled with the settings used by Martyn, were what worked for me: <code>clang-3.5 -fsanitize=undefined -fno-sanitize=float-divide-by-zero,vptr,function -fno-sanitize-recover</code>.</p>
<p>This is now part of the updated <a href="https://github.com/rocker-org/r-devel-san-clang/blob/master/Dockerfile">Dockerfile</a> of the <a href="https://github.com/rocker-org/r-devel-san-clang">R-devel-SAN-Clang repo</a> behind the <a href="https://registry.hub.docker.com/u/rocker/r-devel-ubsan-clang/">r-devel-ubsan-clang</a>. It contains these settings, as well a new support script <a href="https://github.com/eddelbuettel/littler/blob/master/examples/check.r">check.r</a> for <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a>---which enables testing right out the box.</p>
<p>Here is a complete example:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">docker</span>                              <span class="co"># run Docker (any recent version, I use 1.2.0)</span>
  <span class="kw">run</span>                               <span class="co"># launch a container </span>
    <span class="kw">--rm</span>                            <span class="co"># remove Docker temporary objects when dome</span>
    <span class="kw">-ti</span>                             <span class="co"># use a terminal and interactive mode </span>
    <span class="kw">-v</span> <span class="ot">$(</span><span class="kw">pwd</span><span class="ot">)</span>:/mnt                  <span class="co"># mount the current directory as /mnt in the container</span>
    <span class="kw">rocker/r-devel-ubsan-clang</span>      <span class="co"># using the rocker/r-devel-ubsan-clang container</span>
  <span class="kw">check.r</span>                           <span class="co"># launch the check.r command from littler (in the container)</span>
    <span class="kw">--setwd</span> /mnt                    <span class="co"># with a setwd() to the /mnt directory</span>
    <span class="kw">--install-deps</span>                  <span class="co"># installing all package dependencies before the test</span>
    <span class="kw">RcppAnnoy_0.0.5.tar.gz</span>          <span class="co"># and test this tarball</span></code></pre>
<p>I know. It is a mouthful. But it really is <em>merely</em> the standard practice of running Docker to launch a single command. And while I frequently make this the <code>/bin/bash</code> command (hence the <code>-ti</code> options I always use) to work and explore interactively, here we do one better thanks to the (pretty useful so far) <a href="https://github.com/eddelbuettel/littler/blob/master/examples/check.r">check.r</a> script I wrote over the last two days.</p>
<p><a href="https://github.com/eddelbuettel/littler/blob/master/examples/check.r">check.r</a> does about the same as <code>R CMD check</code>. If you look inside <code>check</code> you will see a call to a (non-exported) function from the (R base-internal) <code>tools</code> package. We call the same function here. But to make things more interesting we <em>also</em> first install the package we test to really ensure we have all build-dependencies from CRAN met. (And we plan to extend <code>check.r</code> to support additional <code>apt-get</code> calls in case other libraries etc are needed.) We use the <code>dependencies=TRUE</code> option to have R smartly install <code>Suggests:</code> as well, but only one level (see <code>help(install.packages)</code> for details. With that prerequisite out of the way, the test can proceed as if we had done <code>R CMD check</code> (and additional <code>R CMD INSTALL</code> as well). The result for this (known-bad) package:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ docker run --rm -ti -v <span class="ot">$(</span><span class="kw">pwd</span><span class="ot">)</span>:/mnt rocker/r-devel-ubsan-clang check.r --setwd /mnt --install-deps RcppAnnoy_0.0.5.tar.gz 
<span class="kw">also</span> installing the dependencies ‘Rcpp’, ‘BH’, ‘RUnit’

<span class="kw">trying</span> URL <span class="st">&#39;http://cran.rstudio.com/src/contrib/Rcpp_0.11.3.tar.gz&#39;</span>
<span class="kw">Content</span> type <span class="st">&#39;application/x-gzip&#39;</span> length 2169583 bytes (2.1 MB)
<span class="kw">opened</span> URL
==================================================
<span class="kw">downloaded</span> 2.1 MB

<span class="kw">trying</span> URL <span class="st">&#39;http://cran.rstudio.com/src/contrib/BH_1.55.0-3.tar.gz&#39;</span>
<span class="kw">Content</span> type <span class="st">&#39;application/x-gzip&#39;</span> length 7860141 bytes (7.5 MB)
<span class="kw">opened</span> URL
==================================================
<span class="kw">downloaded</span> 7.5 MB

<span class="kw">trying</span> URL <span class="st">&#39;http://cran.rstudio.com/src/contrib/RUnit_0.4.28.tar.gz&#39;</span>
<span class="kw">Content</span> type <span class="st">&#39;application/x-gzip&#39;</span> length 322486 bytes (314 KB)
<span class="kw">opened</span> URL
==================================================
<span class="kw">downloaded</span> 314 KB

<span class="kw">trying</span> URL <span class="st">&#39;http://cran.rstudio.com/src/contrib/RcppAnnoy_0.0.4.tar.gz&#39;</span>
<span class="kw">Content</span> type <span class="st">&#39;application/x-gzip&#39;</span> length 25777 bytes (25 KB)
<span class="kw">opened</span> URL
==================================================
<span class="kw">downloaded</span> 25 KB

<span class="kw">*</span> installing *source* package ‘Rcpp’ ...
<span class="kw">**</span> package ‘Rcpp’ successfully unpacked and MD5 sums checked
<span class="kw">**</span> libs
<span class="kw">clang++-3.5</span> -fsanitize=undefined -fno-sanitize=float-divide-by-zero,vptr,function -fno-sanitize-recover -I/usr/local/lib/R/include -DNDEBUG -I../inst/include/ -I/usr/local/include    -fpic  -pipe -Wall -pedantic -
<span class="kw">g</span>  -c Date.cpp -o Date.o

[<span class="kw">...</span>]
<span class="kw">*</span> checking examples ... OK
<span class="kw">*</span> checking for unstated dependencies in ‘tests’ ... OK
<span class="kw">*</span> checking tests ...
  <span class="kw">Running</span> ‘runUnitTests.R’
 <span class="kw">ERROR</span>
<span class="kw">Running</span> the tests in ‘tests/runUnitTests.R’ failed.
<span class="kw">Last</span> 13 lines of output:
  <span class="kw">+</span>     if (getErrors(tests)<span class="ot">$nFail</span> <span class="kw">&gt;</span> <span class="kw">0</span>) <span class="kw">{</span>
  <span class="kw">+</span>         stop(<span class="st">&quot;TEST FAILED!&quot;</span>)
  <span class="kw">+</span>     <span class="kw">}</span>
  <span class="kw">+</span>     if (getErrors(tests)<span class="ot">$nErr</span> <span class="kw">&gt;</span> <span class="kw">0</span>) <span class="kw">{</span>
  <span class="kw">+</span>         stop(<span class="st">&quot;TEST HAD ERRORS!&quot;</span>)
  <span class="kw">+</span>     <span class="kw">}</span>
  <span class="kw">+</span>     if (getErrors(tests)<span class="ot">$nTestFunc</span> <span class="kw">&lt;</span> <span class="kw">1</span>) <span class="kw">{</span>
  <span class="kw">+</span>         stop(<span class="st">&quot;NO TEST FUNCTIONS RUN!&quot;</span>)
  <span class="kw">+</span>     <span class="kw">}</span>
  <span class="kw">+</span> }
  
  
  <span class="kw">Executing</span> test function test01getNNsByVector  ... ../inst/include/annoylib.h:532:40: runtime error: index 3 out of bounds for type <span class="st">&#39;int const[2]&#39;</span>
<span class="kw">*</span> checking PDF version of manual ... OK
<span class="kw">*</span> DONE

<span class="kw">Status</span>: 1 ERROR, 2 WARNINGs, 1 NOTE
<span class="kw">See</span>
  ‘<span class="kw">/tmp/RcppAnnoy/..Rcheck</span>/<span class="kw">00check.log</span>’
<span class="kw">for</span> <span class="kw">details.</span>
<span class="kw">root@a7687c014e55</span>:/tmp/RcppAnnoy# </code></pre>
<p>The log shows that thanks to <code>check.r</code>, we first download and the install the required packages Rcpp, BH, RUnit and RcppAnnoy itself (in the CRAN release). Rcpp is installed first, we then cut out the middle until we get to ... the failure we set out to confirm.</p>
<p>Now having a tool to confirm the error, we can work on improved code.</p>
<p>One such fix currently under inspection in a non-release version 0.0.5.1 then passes with the exact same invocation (but pointing at <code>RcppAnnoy_0.0.5.1.tar.gz</code>):</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ docker run --rm -ti -v <span class="ot">$(</span><span class="kw">pwd</span><span class="ot">)</span>:/mnt rocker/r-devel-ubsan-clang check.r --setwd /mnt --install-deps RcppAnnoy_0.0.5.1.tar.gz
<span class="kw">also</span> installing the dependencies ‘Rcpp’, ‘BH’, ‘RUnit’
[<span class="kw">...</span>]
<span class="kw">*</span> checking examples ... OK
<span class="kw">*</span> checking for unstated dependencies in ‘tests’ ... OK
<span class="kw">*</span> checking tests ...
  <span class="kw">Running</span> ‘runUnitTests.R’
 <span class="kw">OK</span>
<span class="kw">*</span> checking PDF version of manual ... OK
<span class="kw">*</span> DONE

<span class="kw">Status</span>: 1 WARNING
<span class="kw">See</span>
  ‘<span class="kw">/mnt/RcppAnnoy.Rcheck</span>/<span class="kw">00check.log</span>’
<span class="kw">for</span> <span class="kw">details.</span>

<span class="kw">edd@max</span>:~/git$</code></pre>
<p>This proceeds the same way from the same pristine, clean container for testing. It first installs the four required packages, and the proceeds to test the new and improved tarball. Which passes the test which failed above with no issues. Good.</p>
<p>So we now have an &quot;appliance&quot; container anybody can download from free from the Docker hub, and deploy as we did here in order to have fully automated, one-command setup for testing for UBSAN errors.</p>
<p>UBSAN is a very powerful tool. We are only beginning to deploy it. There are many more useful configuration settings. I would love to hear from anyone who would like to work on building this out via the <a href="https://github.com/rocker-org/r-devel-san-clang">R-devel-SAN-Clang GitHub repo</a>. Improvements to the <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a> scripts are similarly welcome (and I plan on releasing an updated littler package &quot;soon&quot;).</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
</p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
