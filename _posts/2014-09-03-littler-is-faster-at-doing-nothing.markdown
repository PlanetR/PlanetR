---
title: "littler is faster at doing nothing!"
kind: article
created_at: 2014-09-03 02:25:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>With <a href="http://dirk.eddelbuettel.com/blog/2014/09/01#littler-0.2.0">yesterday's announcement of littler 0.2.0</a>, I kept thinking about a few not-so-frequently-asked but recurring questions about <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a>. And an obvious one if of course the relationship to Rscript.</p>
<p>As we have pointed out before, <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a> preceded Rscript. Now, with Rscript being present in every R installation, it is of course by now more widely known.</p>
<p>But there is one important aspect which I stressed once or twice in the past and which bears repeating. Due to the <em>lean and mean</em> way in which <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a> is designed and set-up, it actually starts a lot faster than either Rscript or R. How, you ask? Well we actually query the environement at build time and hardcode a number of settings which R and Rscript re-acquire and learn each time they start. Which is more flexible. But slower.</p>
<p>So consider the following, really simple example. In it, we create a simple worker function <code>f</code> which launches the given (and simplest possible) R command of just quitting 250 times (by launching a shell command which loops). We then let <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a>, Rscript and R (in its <em>just execute this expression</em> mode) run this, and time it via one of the common benchmarking packages.</p>
<pre class="sourceCode r"><code class="sourceCode r">R&gt;<span class="st"> </span><span class="kw">library</span>(rbenchmark)
R&gt;<span class="st"> </span>f &lt;-<span class="st"> </span>function(cmd) { <span class="kw">system</span>(<span class="kw">paste0</span>(<span class="st">&quot;bash -c </span><span class="ch">\&quot;</span><span class="st">for i in </span><span class="ch">\\</span><span class="st">$(seq 1 250); do &quot;</span>, cmd, <span class="st">&quot; -e &#39;q()&#39;; done</span><span class="ch">\&quot;</span><span class="st">&quot;</span>)); }
R&gt;<span class="st"> </span>res &lt;-<span class="st"> </span><span class="kw">benchmark</span>(<span class="kw">f</span>(<span class="st">&quot;r&quot;</span>), <span class="kw">f</span>(<span class="st">&quot;Rscript&quot;</span>), <span class="kw">f</span>(<span class="st">&quot;R --slave&quot;</span>), <span class="dt">replications=</span><span class="dv">5</span>, <span class="dt">order=</span><span class="st">&quot;relative&quot;</span>)
R&gt;<span class="st"> </span>res
            test replications elapsed relative user.self sys.self user.child sys.child
<span class="dv">1</span>         <span class="kw">f</span>(<span class="st">&quot;r&quot;</span>)            <span class="dv">5</span>  <span class="fl">32.256</span>    <span class="fl">1.000</span>     <span class="fl">0.001</span>    <span class="fl">0.004</span>     <span class="fl">26.538</span>     <span class="fl">5.706</span>
<span class="dv">2</span>   <span class="kw">f</span>(<span class="st">&quot;Rscript&quot;</span>)            <span class="dv">5</span> <span class="fl">180.154</span>    <span class="fl">5.585</span>     <span class="fl">0.001</span>    <span class="fl">0.004</span>    <span class="fl">152.751</span>    <span class="fl">28.522</span>
<span class="dv">3</span> <span class="kw">f</span>(<span class="st">&quot;R --slave&quot;</span>)            <span class="dv">5</span> <span class="fl">302.714</span>    <span class="fl">9.385</span>     <span class="fl">0.001</span>    <span class="fl">0.004</span>    <span class="fl">270.569</span>    <span class="fl">33.098</span>
R&gt;<span class="st"> </span></code></pre>
<p>So there: <a href="http://dirk.eddelbuettel.com/code/littler.html">littler</a> does &quot;nothing&quot; about five times as fast as Rscript, and about nine times as fast as R. Not that this matters greatly -- but when you design something for repeated (unsupervised) execution, say in a cronjob, it might as well be lightweight.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
