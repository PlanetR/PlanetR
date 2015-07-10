---
title: "drat Tutorial: Publishing a package"
kind: article
created_at: 2015-02-23 02:04:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<h3 id="introduction">Introduction</h3>
<p>The <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> package was released earlier this month, and described in a <a href="http://dirk.eddelbuettel.com/blog/2015/02/07#drat_first_steps">first blog post</a>. I received some helpful feedback about what works and what doesn't. For example, <a href="http://www.stat.ubc.ca/~jenny/">Jenny Bryan</a> pointed out that I was not making a clear enough distinction between the role of using <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> to publish code, and using <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> to receive/install code. Very fair point, and somewhat tricky as <a href="http://www.r-project.org">R</a> aims to blur the line between being a <em>user</em> and <em>developer</em> of statistical analyses, and hence packages. Many of us are both. Both the main point is well taken, and this note aims to clarify this issue a little by focusing on the former.</p>
<p>Another point make by <a href="http://www.stat.ubc.ca/~jenny/">Jenny</a> concerns the double use of <em>repository</em>. And indeed, I conflated <em>repository</em> (in the sense of a <a href="https://github.com">GitHub</a> code repository) with <em>repository</em> for a package store used by a package manager. The former, a <em>GitHub repository</em>, is something we use to <em>implement</em> a personal <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> with: A <em>GitHub repository</em> happens to be uniquely identifiable just by its account name, and given an (optional) <code>gh-pages</code> branch also offers a stable and performant webserver we use to deliver packages for <a href="http://www.r-project.org">R</a>. A (personal) <em>code repository</em> on the other hand is something we implement somewhere---possibly via <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> which supports local directories, possibly on a network share, as well as anywhere web-accessible, <em>e.g.</em> via a <em>GitHub repository</em>. It is a little confusing, but I will aim to make the distinction clearer.</p>
<h3 id="just-once-setting-up-a-drat-repository">Just once: Setting up a drat repository</h3>
<p>So let us for the remainder of this post assume the role of a <em>code publisher</em>. Assume you have a package you would like to make available, which may not be on <a href="http://cran.rstudio.com">CRAN</a> and for which you would like to make installation by others easier via <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>. The example below will use an interim version of <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> which I pushed out yesterday (after fixing a bug noticed when pushing the very new <a href="http://dirk.eddelbuettel.com/blog/2015/02/21#rcppapt_0.0.1">RcppAPT</a> package).</p>
<p>For the following, all we assume (apart from having a package to publish) is that you have a <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> directory setup within your git / <a href="https://github.com">GitHub</a> repository. This is not an onerous restriction. First off, you don't have to use git or <a href="https://github.com">GitHub</a> to publish via <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a>: local file stores and other web servers work just as well (and are documented). <a href="https://github.com">GitHub</a> simply makes it easiest. Second, bootstrapping one is trivial: just <a href="https://help.github.com/articles/fork-a-repo/">fork</a> my <a href="https://github.com/eddelbuettel/drat">drat GitHub repository</a> and then <a href="https://help.github.com/articles/fork-a-repo/">create a local clone of the fork</a>.</p>
<p>There is one additional requirement: you need a <code>gh-pages</code> branch. Using the fork-and-clone approach ensures this. Otherwise, if you know your way around git you already know how <a href="https://help.github.com/categories/github-pages-basics/">to create a gh-pages branch</a>.</p>
<p>Enough of the prerequisities. And on towards real fun. Let's ensure we are in the <code>gh-pages</code> branch:</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git/drat(master)$ <span class="kw">git</span> checkout gh-pages
<span class="kw">Switched</span> to branch <span class="st">&#39;gh-pages&#39;</span>
<span class="kw">Your</span> branch is up-to-date with <span class="st">&#39;origin/gh-pages&#39;</span>.
<span class="kw">edd@max</span>:~/git/drat(gh-pages)$ </code></pre>
<h3 id="publish-run-one-drat-command-to-insert-a-package">Publish: Run one drat command to insert a package</h3>
<p>Now, let us assume you have a package to publish. In my case this was version 0.0.1.2 of <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> itself as it contains a fix for the very command I am showing here. So if you want to run this, ensure you have <em>this version of drat</em> as the <a href="http://cran.r-project.org/web/packages/drat/index.html">CRAN version</a> is currently behind at release 0.0.1 (though I plan to correct that in the next few days).</p>
<p>To publish an R package into a <em>code repository</em> created via <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> running on a <em>drat GitHub repository</em>, just run <code>insertPackage(packagefile)</code> which we show here with the optional <code>commit=TRUE</code>. The path to the package can be absolute are relative; the easists is often to go up one directory from the sources to where <code>R CMD build ...</code> has created the package file.</p>
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">edd@max</span>:~/git$ Rscript -e <span class="st">&#39;library(drat); insertPackage(&quot;drat_0.0.1.2.tar.gz&quot;, commit=TRUE)&#39;</span>
[<span class="kw">gh-pages</span> 0d2093a] adding drat_0.0.1.2.tar.gz to drat
 <span class="kw">3</span> files changed, 2 insertions(+), <span class="kw">2</span> deletions(-)
 <span class="kw">create</span> mode 100644 src/contrib/drat_0.0.1.2.tar.gz
<span class="kw">Counting</span> objects: 7, done.
<span class="kw">Delta</span> compression using up to 8 threads.
<span class="kw">Compressing</span> objects: 100% (7/7), <span class="kw">done.</span>
<span class="kw">Writing</span> objects: 100% (7/7), <span class="kw">7.37</span> KiB <span class="kw">|</span> <span class="kw">0</span> bytes/s, done.
<span class="kw">Total</span> 7 (delta 1), <span class="kw">reused</span> 0 (delta 0)
<span class="kw">To</span> git@github.com:eddelbuettel/drat.git
   <span class="kw">206d2fa..0d2093a</span>  gh-pages -<span class="kw">&gt;</span> gh-pages
<span class="kw">edd@max</span>:~/git$ </code></pre>
<p>You can equally well run this as <code>insertPackage(&quot;drat_0.0.1.2.tar.gz&quot;)</code>, then inspect the repo and only then run the git commands <code>add</code>, <code>commit</code> and <code>push</code>. Also note that future versions of <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> will most likely support git operations directly by relying on the very promising <a href="http://cran.rstudio.com/web/packages/git2r/index.html">git2r</a> package. But this just affect package internals, the user-facing call of <em>e.g.</em> <code>insertPackage(&quot;drat_0.0.1.2.tar.gz&quot;, commit=TRUE)</code> will remain unchanged.</p>
<p>And in a nutshell that really is all there is to it. With the newly <em>drat-ed</em> package pushed to your GitHub repository <em>with a single function call), it is available via the automatically-provided <code>gh-pages</code> webserver access to anyone in the world. All they need to do is to point R's package management code (which is built into R itself and used for </em>e.g._ <a href="http://cran.rstudio.com">CRAN</a> and <a href="http://www.bioconductor.org">BioConductor</a> R package repositories) to the new repo---and that is also just a single <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> command. We showed this in the <a href="http://dirk.eddelbuettel.com/blog/2015/02/07#drat_first_steps">first blog post</a> and may expand on it again in a follow-up.</p>
<p>So in summary, that really is all there is to it. After a one-time setup / ensuring you are on the <code>gh-pages</code> branch, all it takes is <em>a single function call from the drat package</em> to publish your package to your <a href="http://dirk.eddelbuettel.com/code/drat.html">drat</a> GitHub repository.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
