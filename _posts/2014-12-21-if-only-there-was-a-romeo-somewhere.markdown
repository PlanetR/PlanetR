---
title: "If only there was a Romeo somewhere ..."
kind: article
created_at: 2014-12-21 17:06:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p><em>Attention: rant coming. You have been warned, and may want to tune out now.</em></p>
<p>So the top of my Twitter timeline just had a re-tweet posting to <a href="http://chrisvoncsefalvay.com/2014/12/20/The-state-of-Julia.html">this marvel on the state of Julia</a>. I should have known better than to glance at it as it comes from someone providing (as per the side-bar) <em>Thought leadership in Big Data, systems architecture</em> and more. Reading something like this violates the first rule of airport book stores: never touch anything from the business school section, especially on (wait for it) <em>leadership</em> or, worse yet, <em>thought leadership</em>.</p>
<p>But it is Sunday, my first cup of coffee still warm (after finalising two R package updates on GitHub, and one upload to <a href="http://cran.r-project.org">CRAN</a>) and so I read on. Only to be mildly appalled by the usual comparison to R based on the same old Fibonacci sequence.</p>
<p>Look, I am as guilty as anyone of using it (for example all over chapter one of my <a href="http://www.rcpp.org/book/">Rcpp book</a>), but at least <em>I try to stress each and every time that this is kicking R where it is down</em> as its (fairly) poor performance on functions calls (that is well-known and documented) <em>obviously</em> gets aggravated by recursive calls. But hey, for the record, let me restate those results. So Julia beats R by a factor of 385. But let's take a closer look.</p>
<p>For <code>n=25</code>, I get R to take 241 milliseconds---as opposed to his 6905 milliseconds---simply by using the same function I use in every workshop, eg last used at <a href="http:/dirk.eddelbuettel.com/presentations.html">Penn in November</a>, which does <em>not</em> use the dreaded <code>ifelse</code> operator:</p>
<pre class="sourceCode r"><code class="sourceCode r">fibR &lt;-<span class="st"> </span>function(n) {
  if (n &lt;<span class="st"> </span><span class="dv">2</span>) <span class="kw">return</span>(n)
  <span class="kw">return</span>(<span class="kw">fibR</span>(n<span class="dv">-1</span>) +<span class="st"> </span><span class="kw">fibR</span>(n<span class="dv">-2</span>))
}</code></pre>
<p>Switching that to the standard C++ three-liner using <a href="http://dirk.eddelbuettel.com/code/rcpp.html">Rcpp</a></p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(Rcpp)
<span class="kw">cppFunction</span>(<span class="st">&#39;int fibCpp(int n) { </span>
<span class="st">  if (n &lt; 2) return(n);  </span>
<span class="st">  return(fibCpp(n-1) + fibCpp(n-2));  </span>
<span class="st">  }&#39;</span>)</code></pre>
<p>and running a standard benchmark suite gets us the usual result of</p>
<pre class="sourceCode r"><code class="sourceCode r">R&gt;<span class="st"> </span><span class="kw">library</span>(rbenchmark)
R&gt;<span class="st"> </span><span class="kw">benchmark</span>(<span class="kw">fibR</span>(<span class="dv">25</span>),<span class="kw">fibCpp</span>(<span class="dv">25</span>),<span class="dt">order=</span><span class="st">&quot;relative&quot;</span>)[,<span class="dv">1</span>:<span class="dv">4</span>]
        test replications elapsed relative
<span class="dv">2</span> <span class="kw">fibCpp</span>(<span class="dv">25</span>)          <span class="dv">100</span>   <span class="fl">0.048</span>    <span class="fl">1.000</span>
<span class="dv">1</span>   <span class="kw">fibR</span>(<span class="dv">25</span>)          <span class="dv">100</span>  <span class="fl">24.674</span>  <span class="fl">514.042</span>
R&gt;<span class="st"> </span></code></pre>
<p>So for the record as we need this later: that is 48 milliseconds for 100 replications, or about 0.48 milliseconds per run.</p>
<p>Now Julia. And of my standard Ubuntu server running the current release 14.10:</p>
<pre class="sh"><code>edd@max:~$ julia
ERROR: could not open file /home/edd//home/edd//etc/julia/juliarc.jl
 in include at boot.jl:238

edd@max:~$ </code></pre>
<p>So wait, what? You guys can't even ensure a working release on what is probably the most popular and common Linux installation? And I get to that after reading a post on the importance of <em>&quot;Community, Community, Community&quot;</em> and you can't even make sure this works on Ubuntu? Really?</p>
<p>So a little bit of googling later, I see that <code>julia -f</code> is my friend for this flawed release, and I can try to replicate the original timing</p>
<pre class="sh"><code>edd@max:~$ julia -f
               _
   _       _ _(_)_     |  A fresh approach to technical computing
  (_)     | (_) (_)    |  Documentation: http://docs.julialang.org
   _ _   _| |_  __ _   |  Type &quot;help()&quot; to list help topics
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 0.2.1 (2014-02-11 06:30 UTC)
 _/ |\__&#39;_|_|_|\__&#39;_|  |  
|__/                   |  x86_64-linux-gnu

julia&gt; fib(n) = n &lt; 2 ? n : fib(n - 1) + fib(n - 2)
fib (generic function with 1 method)

julia&gt; @elapsed fib(25)
0.002299559

julia&gt; </code></pre>
<p>Interestingly the posts author claims <em>18 milliseconds</em>. I see 2.3 milliseconds here. Maybe someone is having a hard time comparing things to the right of the decimal point. Or maybe his computer is an order of magnitude slower than mine. The more important thing is that Julia is of course faster than R (no surprise: LLVM at work) but also still a lot slower than a (trivial to write and deploy) C++ function. Nothing new here.</p>
<p>So let's recap. Comparison to R was based on a flawed version of a function we only use when we deliberately want to put R down, can be improved significantly when using a better implementation, results are still off by order of magnitude to what was reported (&quot;math is hard&quot;), and the standard C / C++ way of doing things is still several times faster than our new saviour language---which I can't even launch on the current version of one of the more common free operating systems. Ok then. Someone please wake me up in a few years and I will try again.</p>
<p>Now, coming to the end of the rant I should really stress that <em>of course</em> I too hope that Julia succeeds. Every user pulled away from Matlab is a win for all us. We're in this <em>together</em> and the endless navel gazing between ourselves is so tiresome and irrelevant. And as I argue here, even more so when we among ourselves stick to unfair comparisons as well as badly chosen implementation details.</p>
<p>What matters are wins against the likes of Matlab, Excel, SAS and so on. Let's build on our <em>joint strength</em>. I am sure I will use Julia one day, and I am grateful for everyone helping with it---as a lot of help seems to be needed. In the meantime, and with <a href="http://cran.r-project.org">CRAN</a> at 6130 packages <em>that just work</em> I'll continue to make use of this amazing community and trying my bit to help it grow and prosper. As part of our joint community.</p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
