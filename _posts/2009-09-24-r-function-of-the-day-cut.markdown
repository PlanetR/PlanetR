---
title: "R Function of the Day: cut"
kind: article
created_at: 2009-09-24 04:18:06 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
The <b>R Function of the Day</b> series will focus on describing in <i>plain language</i> how certain <a href="http://www.R-project.org">R</a> functions work, focusing on simple examples that you can apply to gain insight into your own data.
</p>
<p>
Today, I will discuss the <a href="http://finzi.psych.upenn.edu/R/library/base/html/cut.html"><b>cut</b></a> function.
</p>
<div id="outline-container-1.1" class="outline-3">
<h3 id="sec-1.1">What situation is cut useful in? </h3>
<div id="text-1.1">
<p>
In many data analysis settings, it might be useful to break up a continuous variable such as age into a categorical variable.  Or, you might want to classify a categorical variable like year into a larger bin, such as 1990-2000.  There are <a href="http://biostat.mc.vanderbilt.edu/twiki/bin/view/Main/CatContinuous">many</a> <a href="http://www.stat.columbia.edu/~cook/movabletype/archives/2008/01/debate_over_cat.html">reasons</a> <i>not</i> to do this when performing regression analysis, but for simple displays of demographic data in tables, it could make sense.  The <b>cut</b> function in R makes this task simple!
</p>
</div>
</div>
<div id="outline-container-1.2" class="outline-3">
<h3 id="sec-1.2">How do I use cut? </h3>
<div id="text-1.2">
<p>
First, we will simulate some data from a hypothetical clinical trial that includes variables for patient ID, age, and year of enrollment.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## generate data for clinical trial example
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> clinical.trial <span style="color:#5f9ea0;">&lt;-</span>
    data.frame(patient = 1:100,              
               age = rnorm(100, mean = 60, sd = 8),
               year.enroll = sample(paste(<span style="color:#b22222;">"19"</span>, 85:99, sep = <span style="color:#b22222;">""</span>),
                 100, replace = <span style="color:#0a6;">TRUE</span>))
<span style="color:#a020f0;font-weight:bold;">&gt;</span> summary(clinical.trial)
    patient            age         year.enroll
 Min.   :  1.00   Min.   :41.18   1991   :12  
 1st Qu.: 25.75   1st Qu.:52.99   1988   :11  
 Median : 50.50   Median :60.08   1985   : 9  
 Mean   : 50.50   Mean   :59.67   1993   : 7  
 3rd Qu.: 75.25   3rd Qu.:65.67   1995   : 7  
 Max.   :100.00   Max.   :76.40   1997   : 7  
                                  (Other):47   

</pre>
<p>
Now, we will use the <b>cut</b> function to make age a factor, which is what R calls a categorical variable. Our first example calls cut with the <b>breaks</b> argument set to a single number.  This method will cause <b>cut</b> to break up age into 4 intervals.  The default labels use standard <a href="http://en.wikipedia.org/wiki/Interval_(mathematics)#Notations_for_intervals">mathematical notation</a> for open and closed intervals.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## basic usage of cut with a numeric variable
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> c1 <span style="color:#5f9ea0;">&lt;-</span> cut(clinical.trial$age, breaks = 4)
<span style="color:#a020f0;font-weight:bold;">&gt;</span> table(c1)
c1
  (41.1,50]   (50,58.8] (58.8,67.6] (67.6,76.4] 
          9          34          41          16  
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## year.enroll is a factor, so must convert to numeric first!
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> c2 <span style="color:#5f9ea0;">&lt;-</span> cut(as.numeric(as.character(clinical.trial$year.enroll)),
            breaks = 3)
<span style="color:#a020f0;font-weight:bold;">&gt;</span> table(c2)
c2
(1985,1990] (1990,1994] (1994,1999] 
         36          34          30  

</pre>
<p>
Well, the intervals that <b>cut</b> chose by default are not the nicest looking with the age example, although they are fine with the year example, since it was already discrete. Luckily, we can specify the exact intervals we want for age.  Our next example shows how.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## specify break points explicitly using seq function
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> 
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## look what seq does  
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> seq(30, 80, by = 10)
<span style="color:#5f9ea0;">[1]</span> 30 40 50 60 70 80 
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## cut the age variable using the seq defined above
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> c1 <span style="color:#5f9ea0;">&lt;-</span> cut(clinical.trial$age, breaks = seq(30, 80, by = 10))
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## table of the resulting factor           
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> table(c1)
c1
(30,40] (40,50] (50,60] (60,70] (70,80] 
      0       9      40      42       9  

</pre>
<p>
That looks pretty good.  There is no reason that the breaks argument has to be equally spaced as I have done above.  It could be any grouping that you want.
</p>
<p>
Finally, I am going to show you an example of a custom R function to categorize ages.  It uses <b>cut</b> inside of it, but does some preprocessing and uses the <b>labels</b> argument to cut to make the output look nice.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">
<span style="color:#0000ff;font-weight:bold;">age.cat</span> <span style="color:#5f9ea0;">&lt;-</span> function(x, lower = 0, upper, by = 10,
                   sep = <span style="color:#b22222;">"-"</span>, above.char = <span style="color:#b22222;">"+"</span>) {

 labs <span style="color:#5f9ea0;">&lt;-</span> c(paste(seq(lower, upper - by, by = by),
                 seq(lower + by - 1, upper - 1, by = by),
                 sep = sep),
           paste(upper, above.char, sep = <span style="color:#b22222;">""</span>))

 cut(floor(x), breaks = c(seq(lower, upper, by = by), <span style="color:#0a6;">Inf</span>),
     right = <span style="color:#0a6;">FALSE</span>, labels = labs)
}
</pre>
<p>
This function categorizes age in a fairly flexible way.  The first assignment to <b>labs</b> inside the function creates a vector of labels. Then, the <b>cut</b> function is called to do the work, with the custom labels as an argument.  Here are some examples using our simulated data from above. I am no longer going to save the results of the function calls to a variable and call <b>table</b> on them, but rather just nest the call to <b>age.cat</b> in a call to <b>table</b>. I previously did a post on the <a href="https://blogisticreflections.wordpress.com/2009/09/21/r-function-of-the-day-table/">table</a> function.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## only specifying an upper bound, uses 0 as lower bound, and
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## breaks up categories by 10
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> table(age.cat(clinical.trial$age, upper = 70))
  0-9 10-19 20-29 30-39 40-49 50-59 60-69   70+ 
    0     0     0     0     9    40    42     9  
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## now specifying a lower bound
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> table(age.cat(clinical.trial$age, lower = 30, upper = 70))
30-39 40-49 50-59 60-69   70+ 
    0     9    40    42     9  
<span style="color:#a020f0;font-weight:bold;">&gt;</span> <span style="color:#0a0;font-style:italic;">## now specifying a lower bound AND the "by" argument 
</span><span style="color:#a020f0;font-weight:bold;">&gt;</span> table(age.cat(clinical.trial$age, lower = 30, upper = 70, by = 5))
30-34 35-39 40-44 45-49 50-54 55-59 60-64 65-69   70+ 
    0     0     3     6    22    18    22    20     9  

</pre>
</div>
</div>
<div id="outline-container-1.3" class="outline-3">
<h3 id="sec-1.3">Summary of cut </h3>
<div id="text-1.3">
<p>
The cut function is useful for turning continuous variables into factors.  You saw how to specify the number of cutpoints, specify the exact cutpoints, and saw a function built around <b>cut</b> that simplifies  categorizing an age variable and giving it appropriate labels.
</p>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/94/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/94/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=94&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
