---
title: "R Function of the Day: rle"
kind: article
created_at: 2009-09-23 01:13:18 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
The <b>R Function of the Day</b> series will focus on describing in <i>plain language</i> how certain <a href="http://www.R-project.org">R</a> functions work, focusing on simple examples that you can apply to gain insight into your own data.
</p>
<p>
Today, I will discuss the <a href="http://finzi.psych.upenn.edu/R/library/base/html/rle.html"><b>rle</b></a> function.
</p>
<div id="outline-container-1.1" class="outline-3">
<h3 id="sec-1.1">What situation is rle useful in? </h3>
<div id="text-1.1">
<p>
The <b>rle</b> function is named for the acronym of &#8220;run length encoding&#8221;. What does the term &#8220;run length&#8221; mean?  Imagine you <a href="http://www.codingthewheel.com/archives/the-coin-flip-a-fundamentally-unfair-proposition">flip a coin</a> 10 times and record the outcome as &#8220;H&#8221; if the coin lands showing heads, and &#8220;T&#8221; if the coin lands showing tails.  You want to know what the longest streak of heads is.  You also want to know the longest streak of tails.  The <i>run length</i> is the length of consecutive types of a flip.  If the outcome of our experiment was &#8220;H T T H H H H H T H&#8221;, the longest run length of heads would be 5, since there are 5 consecutive heads starting at position 4, and the longest run length for tails would be 2, since there are two consecutive heads starting at position 2. If you just have 10 flips, it is pretty easy to simply eyeball the answer.  But if you had 100 flips, or 100,000, it would not be easy at all.  However, it is very easy with the <b>rle</b> function in R! That function will <i>encode</i> the entire result into its run lengths.  Using the example above, we start with 1 H, then 2 Ts, 5 Hs, 1 T, and finally 1 H.  That is exactly what the <b>rle</b> function computes, as you will see below in the example.
</p>
</div>
</div>
<div id="outline-container-1.2" class="outline-3">
<h3 id="sec-1.2">How do I use rle? </h3>
<div id="text-1.2">
<p>
First, we will simulate the results of a the coin flipping experiment.  This is trivial in R using the <b>sample</b> function. We simulate flipping a coin 1000 times.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## generate data for coin flipping example 
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> coin <span style="color:#5f9ea0;">&lt;-</span> sample(c(<span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"T"</span>), 1000, replace = <span style="color:#0a6;">TRUE</span>)
<span style="color:#a020f0;font-weight:bold;">&gt;</span> table(coin) 
coin
  H   T 
501 499  
<span style="color:#a020f0;font-weight:bold;">&gt;</span> head(coin, n = 20)
 <span style="color:#5f9ea0;">[1]</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span>
<span style="color:#5f9ea0;">[15]</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"H"</span> 

</pre>
<p>
We can see the results of the first 20 tosses by using the <b>head</b> (as in &#8220;beginning&#8221;, nothing to do with coin tosses) function on our <b>coin</b> vector.
</p>
<p>
So, our question is, what is the longest run of heads, and longest run of tails?  First, what does the output of the <b>rle</b> function look like?
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## use the rle function on our SMALL EXAMPLE above
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## note results MATCH what I described above... 
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> rle(c(<span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"T"</span>, <span style="color:#b22222;">"T"</span>, <span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"H"</span>, <span style="color:#b22222;">"T"</span>, <span style="color:#b22222;">"H"</span>))
Run Length Encoding
  lengths: int [1:5] 1 2 5 1 1
  values : chr [1:5] <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> 
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## use the rle function on our SIMULATED data
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> coin.rle <span style="color:#5f9ea0;">&lt;-</span> rle(coin)
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## what is the structure of the returned result? 
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> str(coin.rle)
List of 2
 $ lengths: int [1:500] 1 1 3 1 1 1 2 1 1 1 ...
 $ values : chr [1:500] <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> <span style="color:#b22222;">"T"</span> <span style="color:#b22222;">"H"</span> ...
 - attr(*, <span style="color:#b22222;">"class"</span>)= chr <span style="color:#b22222;">"rle"</span> 
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## sort the data, this shows the longest run of
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## ANY type (heads OR tails)
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> sort(coin.rle$lengths, decreasing = <span style="color:#0a6;">TRUE</span>)
  <span style="color:#5f9ea0;">[1]</span> 9 8 7 7 7 7 7 6 6 6 6 6 6 6 6 5 5 5 5 5 5 5 5 5 5 5 5
 <span style="color:#5f9ea0;">[28]</span> 5 5 5 5 5 5 5 5 5 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
 <span style="color:#5f9ea0;">[55]</span> 4 4 4 4 4 4 4 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
 <span style="color:#5f9ea0;">[82]</span> 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
<span style="color:#5f9ea0;">[109]</span> 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 2 2 2 2 2 2 2
<span style="color:#5f9ea0;">[136]</span> 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
<span style="color:#5f9ea0;">[163]</span> 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
<span style="color:#5f9ea0;">[190]</span> 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
<span style="color:#5f9ea0;">[217]</span> 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
<span style="color:#5f9ea0;">[244]</span> 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[271]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[298]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[325]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[352]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[379]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[406]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[433]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[460]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
<span style="color:#5f9ea0;">[487]</span> 1 1 1 1 1 1 1 1 1 1 1 1 1 1 
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## use the tapply function to break up
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## into 2 groups, and then find the maximum
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## within each group
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> 
<span style="color:#a020f0;font-weight:bold;">&gt;</span> tapply(coin.rle$lengths, coin.rle$values, max)
H T 
9 8  

</pre>
<p>
So in this case the longest run of heads is 9 and the longest run of tails is 8.  The <a href="https://blogisticreflections.wordpress.com/2009/09/20/r-function-of-the-day-tapply/#"><b>tapply</b></a> function was discussed in a previous <b>R Function of the Day</b> article.
</p>
</div>
</div>
<div id="outline-container-1.3" class="outline-3">
<h3 id="sec-1.3">Summary of rle </h3>
<div id="text-1.3">
<p>
The <b>rle</b> function performs run length encoding.  Although it is not used terribly often when programming in R, there are certain situations, such as time series and longitudinal data analysis, where knowing how it works can save a lot of time and give you insight into your data.
</p>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/70/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/70/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=70&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
