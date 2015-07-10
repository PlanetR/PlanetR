---
title: "Emacs Key Binding for eval-defun in lisp-mode"
kind: article
created_at: 2009-09-23 03:50:46 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
When I use <a href="http://www.R-project.org">R</a> in Emacs through the <a href="http://ess.r-project.org">ESS</a> package, C-c C-c in a .R buffer will send a &#8220;block&#8221; of code to the inferior R process for evaluation.  This was added just a few years ago, but my fingers are now trained to use that key combination for evaluating any block of code.  Since I have been learning Emacs Lisp, I decided that a good idea would be to make C-c C-c a binding to <a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Lisp-Eval.html"><b>eval-defun</b></a>.  I really like how it is working out as I have to redefine my Lisp functions many times! <span class='wp-smiley wp-emoji wp-emoji-smile' title=':-)'>:-)</span>
</p>
<p>
Just put the following in your .emacs file to get this behavior. However, please note the following from the <b>eval-defun</b> help string, &#8220;If the current defun is actually a call to `defvar&#8217; or `defcustom&#8217;, evaluating it this way resets the variable using its initial value expression even if the variable already has some other value. (Normally `defvar&#8217; and `defcustom&#8217; do not alter the value if there already is one.)&#8221;
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;" class="src src-emacs-lisp">
(define-key lisp-mode-shared-map <span style="color:#b22222;">"\C-c\C-c"</span> 'eval-defun) 
</pre><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/86/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/86/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=86&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
