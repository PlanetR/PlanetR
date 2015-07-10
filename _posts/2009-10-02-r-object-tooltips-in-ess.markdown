---
title: "R Object Tooltips in ESS"
kind: article
created_at: 2009-10-02 03:27:54 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
Whether at work or for personal projects, I use <a href="http://ess.r-project.org">ESS</a> a lot to perform interactive data analyses. The ability to write, edit, and submit R commands to an interactive R process is simply something I cannot imagine analyzing data without.
</p>
<div id="outline-container-1.1" class="outline-3">
<h3 id="sec-1.1">An example </h3>
<div id="text-1.1">
<p>
One thing that I end up having to do a lot is inspect an object that I have just assigned to a variable in R.  To fix ideas, let us create a data.frame called <b>df</b> for this example.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> df <span style="color:#5f9ea0;">&lt;-</span> data.frame(patient = 1:100,
                   age = rnorm(100, mean = 10, sd = 6),
                   sex = sample(gl(2, 50, labels =
                     c(<span style="color:#b22222;">"Male"</span>, <span style="color:#b22222;">"Female"</span>))))


</pre>
<p>
I just created the data.frame <b>df</b>, and I want to know if I did it correctly.  For instance, does it look like I expect it to? Does it have 100 observations like I want?  Do the variables have the right names?  Is the sex variable a factor with two levels?  In short, I want to call the <a href="http://finzi.psych.upenn.edu/R/library/utils/html/str.html"><b>str</b></a> function using the object <b>df</b> as an argument.
</p>
<p>
Here is the output I am interested in seeing:
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-R-transcript">

<span style="color:#a020f0;font-weight:bold;">&gt;</span> str(df)
'data.frame':   100 obs. of  3 variables:
 $ patient: int  1 2 3 4 5 6 7 8 9 10 ...
 $ age    : num  11.06 7.73 17.61 3.11 6.76 ...
 $ sex    : Factor w/ 2 levels <span style="color:#b22222;">"Male"</span>,<span style="color:#b22222;">"Female"</span>: 2 1 1 2 2 1 1 2 2 2 ... 

</pre>
</div>
</div>
<div id="outline-container-1.2" class="outline-3">
<h3 id="sec-1.2">Inspecting objects the old way </h3>
<div id="text-1.2">
<p>
So, how can I quickly see the structure as shown above?  One idea is to switch over to my interactive <b>R</b> buffer in Emacs, type the command at the prompt, and then switch back to my code buffer to edit the data.frame command or continue programming. I dislike having to switch back and forth between the buffers for a one-off command though.
</p>
<p>
Alternatively, I could type <b>str(df)</b> in my code buffer, evaluate it, and decide to keep it or delete the line.  Since this is more of a quick check, without permanent results, I usually will not want to keep lines like this around, since they clutter up my program.  Typically, I am writing the program to be later run in BATCH mode, so I also do not want functions like that in my code since some can be excessively time-consuming depending on the size of the data.frame.
</p>
<p>
Another option is to use the ESS function <b>ess-execute-in-tb</b>, by default this is bound to C-c C-t, which will prompt me for an expression to evaluate.  This is nice because I do not have to clutter my buffer with extraneous function calls.  However, after using this method for a while, I noticed that I had many patterns with my objects.  For data.frames, I would almost always use summary or str on them after assignment.  For factors, I would want to table the values after I created them, to be sure they looked right.  For numeric vectors, I would want to summarize them.  I also wanted to summarize model fits (e.g., <b>lm</b>).  I wanted to take advantage of my usage patterns so that I did not have to type so much after assigning an object to a variable.
</p>
</div>
</div>
<div id="outline-container-1.3" class="outline-3">
<h3 id="sec-1.3">Inspecting objects the new way </h3>
<div id="text-1.3">
<p>
I therefore wrote an Emacs Lisp function that, when called via a key chord in Emacs, inspects the object at point, determines the class of that object, and based on the class, calls an R function on that object, showing the results in a tooltip.  For the <b>df</b> example above, I would just put point on &#8220;df&#8221;, <i>anywhere</i> in the source code, and type C-c C-g (my default binding). A tooltip is then shown with the output of <b>str(df)</b>.
</p>
<p>
An example similar to this, along with several others are shown in this screencast. I think this is the best way to show how my Lisp function interacts with R to show object information in tooltips.
</p>
<span class='embed-youtube' style='text-align:center; display: block;'><iframe class='youtube-player' type='text/html' width='450' height='284' src='https://www.youtube.com/embed/E_N-RXW2_Xo?version=3&#038;rel=1&#038;fs=1&#038;showsearch=0&#038;showinfo=1&#038;iv_load_policy=1&#038;wmode=transparent' frameborder='0' allowfullscreen='true'></iframe></span>
<p>
Pretty nice! One thing to note is that the tooltips are displaying in a proportional font, not a monospace one.  I know at some point I had found a customizable variable to specify which font tooltips display in, but I apparently did not save it. If I find that variable, I will update this post to reflect how to do that.
</p>
</div>
</div>
<div id="outline-container-1.4" class="outline-3">
<h3 id="sec-1.4">The Emacs Lisp function and keybinding </h3>
<div id="text-1.4">
<p>
Here is the code you will need for this behavior.  It depends on having <b>tooltip-show-at-point</b> defined, which is found only in ESS 5.4 (the current version as of this post) or later.  I contributed <b>tooltip-show-at-point</b> to the ESS project a few months ago.  It is used to show argument tooltips when you type an opening parenthesis.  Perhaps my object tooltip function will find its way into a future version of ESS.  Here is the code.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;overflow:auto;" class="src src-emacs-lisp">
<span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">ess-R-object-tooltip.el
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">I have defined a function, ess-R-object-tooltip, that when 
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">invoked, will return a tooltip with some information about
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">the object at point.  The information returned is 
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">determined by which R function is called.  This is controlled
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">by an alist, called ess-R-object-tooltip-alist.  The default is
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">given below.  The keys are the classes of R object that will
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">use the associated function.  For example, when the function
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">is called while point is on a factor object, a table of that
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">factor will be shown in the tooltip.  The objects must of course
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">exist in the associated inferior R process for this to work.
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">The special key "other" in the alist defines which function
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">to call when the class is not mached in the alist.  By default,
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">the str function is called, which is actually a fairly useful
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">default for data.frame and function objects. 
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">The last line of this file shows my default keybinding. 
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">I simply save this file in a directory in my load-path
</span><span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">and then place (require 'ess-R-object-tooltip) in my .emacs 
</span>
<span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">the alist
</span>(setq ess-R-object-tooltip-alist
      '((numeric    . <span style="color:#b22222;">"summary"</span>)
        (factor     . <span style="color:#b22222;">"table"</span>)
        (integer    . <span style="color:#b22222;">"summary"</span>)
        (lm         . <span style="color:#b22222;">"summary"</span>)
        (other      . <span style="color:#b22222;">"str"</span>)))


(<span style="color:#a020f0;font-weight:bold;">defun</span> <span style="color:#0000ff;font-weight:bold;">ess-R-object-tooltip</span> ()
  <span style="color:#c0c;font-style:italic;">"Get info for object at point, and display it in a tooltip."</span>
  (interactive)
  (<span style="color:#a020f0;font-weight:bold;">let</span> ((objname (current-word))
        (curbuf (current-buffer))
        (tmpbuf (get-buffer-create <span style="color:#b22222;">"**ess-R-object-tooltip**"</span>)))
    (<span style="color:#a020f0;font-weight:bold;">if</span> objname
        (<span style="color:#a020f0;font-weight:bold;">progn</span>
          (ess-command (concat <span style="color:#b22222;">"class("</span> objname <span style="color:#b22222;">")\n"</span>)  tmpbuf )   
          (set-buffer tmpbuf)
          (<span style="color:#a020f0;font-weight:bold;">let</span> ((bs (buffer-string)))
            (<span style="color:#a020f0;font-weight:bold;">if</span> (not(string-match <span style="color:#b22222;">"</span><span style="color:#b22222;font-weight:bold;">\</span><span style="color:#b22222;font-weight:bold;">(</span><span style="color:#b22222;">object .* not found</span><span style="color:#b22222;font-weight:bold;">\</span><span style="color:#b22222;font-weight:bold;">)</span><span style="color:#b22222;font-weight:bold;">\</span><span style="color:#b22222;font-weight:bold;">|</span><span style="color:#b22222;">unexpected"</span> bs))
                (<span style="color:#a020f0;font-weight:bold;">let*</span> ((objcls (buffer-substring 
                                (+ 2 (string-match <span style="color:#b22222;">"\".*\""</span> bs)) 
                                (- (point-max) 2)))
                       (myfun (cdr(assoc-string objcls 
                                                ess-R-object-tooltip-alist))))
                  (<span style="color:#a020f0;font-weight:bold;">progn</span>
                    (<span style="color:#a020f0;font-weight:bold;">if</span> (eq myfun nil)
                        (setq myfun 
                              (cdr(assoc-string <span style="color:#b22222;">"other"</span> 
                                                ess-R-object-tooltip-alist))))
                    (ess-command (concat myfun <span style="color:#b22222;">"("</span> objname <span style="color:#b22222;">")\n"</span>) tmpbuf)
                    (<span style="color:#a020f0;font-weight:bold;">let</span> ((bs (buffer-string)))
                      (<span style="color:#a020f0;font-weight:bold;">progn</span>
                        (set-buffer curbuf)
                        (tooltip-show-at-point bs 0 30)))))))))
    (kill-buffer tmpbuf)))

<span style="color:#0a0;">;; </span><span style="color:#0a0;font-style:italic;">my default key map
</span>(define-key ess-mode-map <span style="color:#b22222;">"\C-c\C-g"</span> 'ess-R-object-tooltip)

(<span style="color:#a020f0;font-weight:bold;">provide</span> '<span style="color:#5f9ea0;">ess-R-object-tooltip</span>)
</pre>
<p>
Notice that you can add your own object classes and functions fairly easily at the top of the program. There is a special &#8220;other&#8221; class which will be called for classes not defined otherwise.
</p>
</div>
</div>
<div id="outline-container-1.5" class="outline-3">
<h3 id="sec-1.5">Further meta-data features in ESS? </h3>
<div id="text-1.5">
<p>
If you can think if anymore examples for types of objects that this would be useful for, feel free to post them in the comments. I think this is a very useful feature when interactively examining datasets, fitting models, and analyzing data. In general, I think there are many more interesting ways to have meta-data on objects available quickly within the ESS and R system.  I will be sure to share them as I explore ways to more efficiently do statistical analysis within the R environment.
</p>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/100/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/100/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=100&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
