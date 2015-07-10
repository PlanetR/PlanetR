---
title: "Introduction to using R with org-babel, Part 1"
kind: article
created_at: 2010-05-24 04:12:32 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
In my opinion, the description of <a href="http://orgmode.org">orgmode</a> by its creator as a tool &#8220;for keeping notes, maintaining ToDo lists, doing project planning, and authoring with a fast and effective plain-text system&#8221; is a little like describing Emacs as a &#8220;text editor&#8221;.  While technically accurate, one not acquainted with orgmode might not be immediately persuaded to learn it based on its pedestrian description.  Needless to say, I think it is worthwhile.
</p>
<p>
While there are plenty of <a href="http://orgmode.org/worg/org-tutorials/index.php">tutorials</a> and a great <a href="http://orgmode.org/orgguide.pdf">introduction</a> to orgmode on its site, there exists a relatively new orgmode extension called <a href="http://orgmode.org/worg/org-contrib/babel/index.php">org-babel</a> whose documentation, although complete and accurate, might benefit from a high-level overview showing how it can be used to write an R program in an orgmode buffer.
</p>
<div id="outline-container-1_1" class="outline-3">
<h3 id="sec-1_1">What can orgmode do with source code? </h3>
<div class="outline-text-3" id="text-1_1">
<p>
Even without org-babel, you can <a href="http://orgmode.org/manual/Literal-examples.html#Literal-examples">create a source code block</a> in an orgmode buffer.  Why would you want to do this?  Mostly so that when you export the orgmode buffer to HTML, that the source code <i>looks like</i> source code.  Source code will be displayed in a monospace font, and colored to look just like it does in your Emacs buffer.
</p>
<p>
To accomplish this, you would put something like the following in your org-mode document. I will use the programming language R as an example.  To define a source code block, simply use the #+BEGIN_SRC syntax along with the major mode of the language, in this case &#8216;R&#8217;.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">#+BEGIN_SRC R
x &lt;- 1:5

square &lt;- function(x) {
  x^2
}

square(x)
#+END_SRC
</pre>
<p>
Then, when you export the orgmode document to, say, HTML, your R code will look just as it does in Emacs with syntax highlighting, and will be offset from the text surrounding it, like this:
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">x <span style="color:#5f9ea0;">&lt;-</span> 1:5

<span style="color:#0000ff;font-weight:bold;">square</span> <span style="color:#5f9ea0;">&lt;-</span> <span style="color:#a020f0;font-weight:bold;">function</span>(x) {
  x^2
}

square(x)
</pre>
</div>
<div id="outline-container-1_1_1" class="outline-4">
<h4 id="sec-1_1_1">A note about syntax highlighting in Emacs </h4>
<div class="outline-text-4" id="text-1_1_1">
<p>Ideally, when you entered into a code block, Emacs would recognize this, and the syntax highlighting within the code block would reflect whatever language you had specified as you typed it. Unfortunately, it is difficult to get Emacs to behave this way, at least with orgmode.  I have investigated <a href="http://www.emacswiki.org/emacs/MultipleModes">several options</a> for doing this, but have run into problems with all of them. Orgmode&#8217;s solution to this is to create an <a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Indirect-Buffers.html">indirect buffer</a> containing the source code you&#8217;re editing when you type C-c &#8216; (i.e., Control-C, then a single quote) in a source code block.  You don&#8217;t have to do this, but it is nice to get your program in a temporary buffer that is set to the right mode. In R, this also means you can use all the usual <a href="http://ess.r-project.org">ESS</a> shortcut keys.
</p>
</div>
</div>
</div>
<div id="outline-container-1_2" class="outline-3">
<h3 id="sec-1_2">What does org-babel add to what orgmode can already do? </h3>
<div class="outline-text-3" id="text-1_2">
<p>
Org-babel lets you execute source code blocks in an orgmode buffer.  Well, what does that mean?  At its simplest, org-babel lets you submit a source code block, like the one above, to an R process, and places the results in the actual orgmode buffer.
</p>
<p>
You activate the additional features that org-babel provides by giving the #+BEGIN_SRC line in an orgmode buffer special arguments, some of which I describe below.  All the available options are described in the <a href="http://orgmode.org/worg/org-contrib/babel/reference.php">org-babel documentation</a>. I will show some basic examples of how to add arguments to a #+BEGIN_SRC line.
</p>
<p>
However, since submitting a code block to a new R process and placing the results in the orgmode buffer is the default behavior of org-babel, you don&#8217;t <i>need</i> to supply any arguments to the source code block for this simple operation.  You simply carry out this process by typing C-c C-c in a source code block.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">#+BEGIN_SRC R
x &lt;- 1:5

square &lt;- function(x) {
  x^2
}

square(x)
#+END_SRC


</pre>
<p>
In your org-mode buffer, with point in the code block, you now type C-c C-c, an R process is started, and the following is placed in the orgmode buffer.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">#+results: |  1 | |  4 | |  9 | | 16 | | 25 |
</pre>
<p>
Since we used the default value for the <i>results</i> argument (i.e., we didn&#8217;t specify anything), org-babel collected the output and put it in an org-table, as shown above.  If you just want the output like it would appear in your ESS R process buffer, you can use the value &#8216;output&#8217; to the <i>results</i> argument, as shown below.  You specify an argument by typing a &#8216;:&#8217;, and then using one of the valid parameter names, typing a space, and then giving the value of the parameter.  So, in the example below, <i>results</i> is the name of the parameter, and we&#8217;re setting its value to &#8216;output&#8217;.  The default value for the <i>results</i> parameter is &#8216;value&#8217;, and gives you the same results as above, i.e., a table of the last results returned by the code block.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">#+BEGIN_SRC R :results output
x &lt;- 1:5

square &lt;- function(x) {
  x^2
}

square(x)
#+END_SRC
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">#+results: : [1]  1  4  9 16 25 
</pre>
<p>
Since we set <i>results</i> to &#8216;output&#8217;, we see the familiar R notation for printing a vector.  The default value, where an org-table is created, would be useful for passing the resulting table to perhaps a different function within the orgmode buffer, even one programmed in another language.  That is a  feature that org-babel supports and encourages, but I will not describe that further here.
</p>
<p>
Personally, I set <i>results</i> to &#8216;output&#8217; to write this entries for this blog, since it shows users what the actual R output will look like.  This is nice, because there is no cutting and pasting of the results!  I can just write my R code in a source code block, and then add a special argument to export the code and results to an HTML file upon exporting in orgmode.  My code block would look like this to accomplish that.  Notice the new argument, <i>exports</i>, and its value &#8216;both&#8217;, as in both the code and its results.
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">#+BEGIN_SRC R :results output :exports both 
x &lt;- 1:5

square &lt;- function(x) {
  x^2
}

square(x)
#+END_SRC
</pre>
<p>
Putting the above code in an orgmode buffer and exporting to HTML will show the following:
</p>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="src src-R">x <span style="color:#5f9ea0;">&lt;-</span> 1:5

<span style="color:#0000ff;font-weight:bold;">square</span> <span style="color:#5f9ea0;">&lt;-</span> <span style="color:#a020f0;font-weight:bold;">function</span>(x) {
  x^2
}

square(x)
</pre>
<pre style="background-color:#F3F5F7;font-size:90%;overflow:auto;border:1pt solid #AEBDCC;padding:5pt;" class="example">
[1]  1  4  9 16 25
</pre>
<p>Indeed, using org-babel in this fashion is how I now generate content for this site.  Compare this approach to what I <a href="https://blogisticreflections.wordpress.com/2009/09/20/welcome-to-blogistic-reflections/">used to be doing with Sweave</a>.  The two approaches are  similar, but I now have a completely contained orgmode approach, where as before I had to preprocess the orgmode buffer with an Sweave function before export.  You can see the difference not only in how I specify code blocks, but also how the appearance of the output has changed.
</p>
<p>
Note that the last thing I still have to do in an Elisp function is to insert inline CSS code to generate the background color and outline of the code and results blocks.  As far as I know, there is no way to do this in orgmode yet, as the HTML output it contains the CSS style information in the HTML header.
</p>
</div>
</div>
<div id="outline-container-1_3" class="outline-3">
<h3 id="sec-1_3">Why do things this way? </h3>
<div class="outline-text-3" id="text-1_3">
<p>
I think org-babel is interesting for several reasons.  First, as R was one of the first languages supported by it, and I use R as my main programming language at my job, I was naturally interested in it.  Org-babel is very useful for me because I am used to working in orgmode, so I can add links, tags, TODO items, create notes, and more right in my code.  It&#8217;s like having a hyper-commenting system that can be crosslinked with everything.  Using orgmode&#8217;s intuitive visibility cycling system results in a powerful code-folding feature.  Orgmode properties allow me to collect meta-information about my code, such as what objects a code block create.
</p>
<p>
The export feature of orgmode is very useful for producing this blog, and producing readable documentation for my source code. Also, if I am writing a program to be run in a script, a very common task, org-babel can handle that through a feature called <a href="http://orgmode.org/worg/org-contrib/babel/intro.php#literate-programming">tangling</a>, which I will cover in a future article. The tangling feature turns orgmode into a tool to perform literate programming.
</p>
</div>
</div>
<div id="outline-container-1_4" class="outline-3">
<h3 id="sec-1_4">What is left to cover? </h3>
<div class="outline-text-3" id="text-1_4">
<p>
In addition to tangling mentioned above, there are several important features that I have not even mentioned in this short introduction.  In the subsequent article, I want to show how I use R with org-babel to include inline images created with R, and how to generate <img src='https://s0.wp.com/latex.php?latex=%5CLaTeX&#038;bg=ffffff&#038;fg=333333&#038;s=0' alt='&#92;LaTeX' title='&#92;LaTeX' class='latex' /> output that can be previewed inline in orgmode documents.  Using org-babel in this manner closely mirrors a &#8216;notebook&#8217; style interactive session such as Mathematica provides.  The other main feature that org-babel provides is using it as a meta-programming language to, say, call R functions using data generated from a shell script or Python program.  Org-babel is a very interesting project that is definitely worth your time to check out, especially if you&#8217;re already an Emacs or orgmode user.  If you&#8217;ve read through this post, you can get started by reading the official <a href="http://orgmode.org/worg/org-contrib/babel/intro.php">org-babel introduction</a>, which will describe what to include in your .emacs file to setup org-babel.
</p>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/167/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/167/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=167&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
