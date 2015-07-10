---
title: "R Function of the Day: sample"
kind: article
created_at: 2010-05-23 06:52:35 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
The <b>R Function of the Day</b> series will focus on describing in <i>plain language</i> how certain <a href="http://www.R-project.org">R</a> functions work, focusing on simple examples<br />
that you can apply to gain insight into your own data.
</p>
<p>
Today, I will discuss the <a href="http://finzi.psych.upenn.edu/R/library/base/html/sample.html"><b>sample</b></a> function.
</p>
<div id="outline-container-1_1" class="outline-3">
<h3 id="sec-1_1">Random Permutations </h3>
<div class="outline-text-3" id="text-1_1">
<p>
In its simplest form, the <b>sample</b> function can be used to return a<br />
random permutation of a vector.  To illustrate this, let&#8217;s create a<br />
vector of the integers from 1 to 10 and assign it to a variable <b>x</b>.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">x <span style="color:#5f9ea0;">&lt;-</span> 1:10
</pre>
<p>
Now, use <b>sample</b> to create a random permutation of the vector x.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">sample(x) 
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
 [1]  3  2  1 10  7  9  4  8  6  5
</pre>
<p>Note that if you give <b>sample</b> a vector of length 1 (e.g., just the<br />
number 10) that it will do the exact same thing as above, that is,<br />
create a random permutation of the integers from 1 to 10.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">sample(10) 
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
 [1] 10  7  4  8  2  6  1  9  5  3
</pre>
</div>
<div id="outline-container-1_1_1" class="outline-4">
<h4 id="sec-1_1_1">Warning! </h4>
<div class="outline-text-4" id="text-1_1_1">
<p>
This can be a source of confusion if you&#8217;re not careful.  Consider the<br />
following example from the <b>sample</b> help file.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">sample(x[x &gt; 8])
sample(x[x &gt; 9])
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
[1] 10  9
 [1]  9  3  4  8  1 10  7  5  2  6
</pre>
<p>Notice how the first output is of length 2, since only two numbers are<br />
greater than eight in our vector. But, because of the fact that only<br />
one number (that is, 10) is greater than nine in our vector, <b>sample</b><br />
thinks we want a sample of the numbers from 1 to 10, and therefore<br />
returns a vector of length 10.
</p>
</div>
</div>
</div>
<div id="outline-container-1_2" class="outline-3">
<h3 id="sec-1_2">The <b>replace</b> argument </h3>
<div class="outline-text-3" id="text-1_2">
<p>
Often, it is useful to not simply take a random permutation of a<br />
vector, but rather sample independent draws of the same vector.  For<br />
instance, we can simulate a Bernoulli trial, the result of the flip of<br />
a fair coin.  First, using our previous vector, note that we can tell<br />
<b>sample</b> the size of the sample we want, using the <b>size</b> argument.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">sample(x, size = 5)
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
[1]  2 10  5  1  6
</pre>
<p>Now, let&#8217;s perform our coin-flipping experiment just once.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">coin <span style="color:#5f9ea0;">&lt;-</span> c(<span style="color:#b22222;">"Heads"</span>, <span style="color:#b22222;">"Tails"</span>)
sample(coin, size = 1)
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
[1] "Tails"
</pre>
<p>And now, let&#8217;s try it 100 times.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">sample(coin, size = 100)
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
Error in sample(coin, size = 100) : 
  cannot take a sample larger than the population when 'replace = FALSE'
</pre>
<p>Oops, we can&#8217;t take a sample of size 100 from a vector of size 2,<br />
unless we set the <b>replace</b> argument to TRUE.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">table(sample(coin, size = 100, replace = <span style="color:#0a6;">TRUE</span>))
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">

Heads Tails 
   53    47
</pre>
</div>
</div>
<div id="outline-container-1_3" class="outline-3">
<h3 id="sec-1_3">Simple bootstrap example </h3>
<div class="outline-text-3" id="text-1_3">
<p>
The <b>sample</b> function can be used to perform a simple bootstrap.<br />
Let&#8217;s use it to estimate the 95% confidence interval for the mean of a<br />
population.  First, generate a random sample from a normal<br />
distribution.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">rn <span style="color:#5f9ea0;">&lt;-</span> rnorm(1000, 10)
</pre>
<p>
Then, use <b>sample</b> multiple times using the <b>replicate</b> function to<br />
get our bootstrap resamples. The defining feature of this technique is<br />
that replace = TRUE.  We then take the mean of each new sample, gather them, and finally compute the relevant quantiles.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">quantile(replicate(1000, mean(sample(rn, replace = <span style="color:#0a6;">TRUE</span>))),
         probs = c(0.025, 0.975))
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
     2.5%     97.5% 
 9.936387 10.062525
</pre>
<p>Compare this to the standard parametric technique.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">t.test(rn)$conf.int
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
[1]  9.938805 10.061325
attr(,"conf.level")
[1] 0.95
</pre>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/143/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/143/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=143&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
