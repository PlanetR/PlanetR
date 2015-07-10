---
title: "R Function of the Day: foodweb"
kind: article
created_at: 2010-09-22 04:52:42 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>The <b>R Function of the Day</b> series will focus on describing in <i>plain language</i> how certain <a href="http://www.R-project.org">R</a> functions work, focusing on simple examples<br />
that you can apply to gain insight into your own data.
</p>
<p>
Today, I will discuss the <b>foodweb</b> function, found in the <a href="http://cran.r-project.org/web/packages/mvbutils/index.html">mvbutils</a><br />
package.
</p>
<div id="outline-container-1" class="outline-3">
<h3 id="sec-1">Foodweb?  What is that? </h3>
<div class="outline-text-3" id="text-1">
<p>
In biology, a foodweb is a group of food chains, showing the complex<br />
relationships that exist in nature. Similarly, the R <b>foodweb</b><br />
function contained in the <b>mvbutils</b> package on CRAN displays a<br />
flowchart of function calls.  What functions does my function call?<br />
What funtions in my package call the <b>lm</b> function? These are the<br />
types of questions that can be answered in a graphical way using<br />
<b>foodweb</b>. This information can be useful for documenting your own<br />
code, and for learning how a package that you&#8217;re not familiar with<br />
works. At the end of this post, you&#8217;ll see an example with a diagram<br />
of the <b>survexp</b> function from the survival package.
</p>
<p>
First, you have to install and load the <b>mvbutils</b> package, so let&#8217;s<br />
do that first.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">install.packages(<span style="color:#cc9393;">"mvbutils"</span>)
<span style="color:#dca3a3;font-weight:bold;">library</span>(mvbutils)
</pre>
</div>
</div>
<div id="outline-container-2" class="outline-3">
<h3 id="sec-2">A simple example </h3>
<div class="outline-text-3" id="text-2">
<p>Let&#8217;s define a couple simple functions to see how <b>foodweb</b> works. We<br />
simply define a function called <b>outer</b> that calls two functions,<br />
<b>inner1</b> and <b>inner2</b>.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R"><span style="color:#8cd0d3;">inner1</span> <span style="color:#dca3a3;font-weight:bold;">&lt;-</span> <span style="color:#f0dfaf;font-weight:bold;">function</span>() {
  <span style="color:#cc9393;">"This is the inner1 function"</span>
}

<span style="color:#8cd0d3;">inner2</span> <span style="color:#dca3a3;font-weight:bold;">&lt;-</span> <span style="color:#f0dfaf;font-weight:bold;">function</span>() {
  <span style="color:#cc9393;">"This is the inner2 function"</span>
}

<span style="color:#8cd0d3;">outer</span> <span style="color:#dca3a3;font-weight:bold;">&lt;-</span> <span style="color:#f0dfaf;font-weight:bold;">function</span>(x) {
   i1 <span style="color:#dca3a3;font-weight:bold;">&lt;-</span> inner1()
   i2 <span style="color:#dca3a3;font-weight:bold;">&lt;-</span> inner2()
}  

</pre>
<p>
Now let&#8217;s use the foodweb function to diagram the relationship between<br />
the outer and inner functions. If we don&#8217;t give <b>foodweb</b> any<br />
arguments, it will scour our global workspace for functions, and make<br />
the diagram.  Since the only functions in my global workspace are the<br />
ones we&#8217;ve just defined, we get the following plot.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">foodweb()
</pre>
<p><img src="https://blogisticreflections.files.wordpress.com/2010/09/foodweb13.png?w=450"></p>
<p>
We see a simple graph showing that the outer function calls both the<br />
inner1 and inner2 functions, jus as we expect. We can make this look a<br />
bit nicer by adjusting a few of the arguments.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">foodweb(border = <span style="color:#dfdfbf;font-weight:bold;">TRUE</span>, expand.xbox = 3,
        boxcolor = <span style="color:#cc9393;">"#FC6512"</span>, textcolor = <span style="color:#cc9393;">"black"</span>,
        cex = 1.2, lwd=2)
</pre>
<p><img src="https://blogisticreflections.files.wordpress.com/2010/09/foodweb22.png?w=450"></p>
<p>
You can see that you can control many of the graphical parameters of<br />
the resulting plot. See the help page for <b>foodweb</b> to see the<br />
complete list of graphical parameters you can specify.
</p>
</div>
</div>
<div id="outline-container-3" class="outline-3">
<h3 id="sec-3">A more complicated example </h3>
<div class="outline-text-3" id="text-3">
<p>
As we saw above, by default <b>foodweb</b> will look in your global<br />
workspace for functions to construct the web from.  However, you can<br />
pass <b>foodweb</b> a group of functions to operate on.  There are several<br />
ways of doing this, see the help page for examples.  The code below<br />
shows one possiblity, when we want to limit our results to functions<br />
appearing in a specific package.  The <i>prune</i> argument is very useful.<br />
It takes a string (or regular expression) to prune the resulting graph<br />
to.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">foodweb(where = <span style="color:#cc9393;">"package:survival"</span>, prune = <span style="color:#cc9393;">"survexp"</span>,
        border = <span style="color:#dfdfbf;font-weight:bold;">TRUE</span>,
        expand.xbox = 2, boxcolor = <span style="color:#cc9393;">"#FC6512"</span>,
        textcolor = <span style="color:#cc9393;">"black"</span>, cex = 1.0, lwd=2)
mtext(<span style="color:#cc9393;">"The survexp function foodweb"</span>)
</pre>
<p><img src="https://blogisticreflections.files.wordpress.com/2010/09/foodweb32.png?w=450"></p>
</div>
</div>
<div id="outline-container-4" class="outline-3">
<h3 id="sec-4">Conclusion </h3>
<div class="outline-text-3" id="text-4">
<p>I have used the <b>foodweb</b> function to help understand other user&#8217;s<br />
code that I have inherited. It has proved very valuable in aiding the<br />
comprehension of hard to read or complicated functions. I have also<br />
used it in the development of my own packages, as it sometimes can<br />
suggest ways to reorganize the code to be more logical.
</p>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/179/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/179/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=179&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
