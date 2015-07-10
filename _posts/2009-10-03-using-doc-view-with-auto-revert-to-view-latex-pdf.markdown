---
title: "Using doc-view with auto-revert to view LaTeX PDF output in Emacs"
kind: article
created_at: 2009-10-03 23:24:32 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
When I am authoring a <img src='https://s0.wp.com/latex.php?latex=%5CLaTeX&#038;bg=ffffff&#038;fg=333333&#038;s=0' alt='&#92;LaTeX' title='&#92;LaTeX' class='latex' /> document in Emacs, such as a report or my CV, it is useful for me to compile the <img src='https://s0.wp.com/latex.php?latex=%5CLaTeX&#038;bg=ffffff&#038;fg=333333&#038;s=0' alt='&#92;LaTeX' title='&#92;LaTeX' class='latex' /> source file periodically to see what the resulting file PDF looks like.  I used to run a separate PDF viewer to look at the output, but I now have a complete Emacs solution.
</p>
<div id="outline-container-1.1" class="outline-3">
<h3 id="sec-1.1">The editing environment </h3>
<div id="text-1.1">
<p>
When writing a <img src='https://s0.wp.com/latex.php?latex=%5CLaTeX&#038;bg=ffffff&#038;fg=333333&#038;s=0' alt='&#92;LaTeX' title='&#92;LaTeX' class='latex' /> document, I usually want the output to be a PDF file.  Accordingly, I put the following in my .emacs file.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;" class="src src-emacs-lisp">
(setq TeX-PDF-mode t)
</pre>
<p>
I then split my Emacs frame into two buffers vertically, using C-x 3 (see screencast below).  After compiling my <img src='https://s0.wp.com/latex.php?latex=%5CLaTeX&#038;bg=ffffff&#038;fg=333333&#038;s=0' alt='&#92;LaTeX' title='&#92;LaTeX' class='latex' /> file with C-c C-c, I visit the resulting PDF file in the other Emacs window.  The Emacs <a href="http://www.emacswiki.org/emacs/DocViewMode">doc-view package</a> will display the PDF file.
</p>
</div>
</div>
<div id="outline-container-1.2" class="outline-3">
<h3 id="sec-1.2">Including auto-revert functionality </h3>
<div id="text-1.2">
<p>
The final piece to the puzzle is to set files visited in doc-view-mode to <a href="http://www.emacswiki.org/emacs/RevertBuffer">auto-revert</a> when changed on disk.  That way, then I update my <img src='https://s0.wp.com/latex.php?latex=%5CLaTeX&#038;bg=ffffff&#038;fg=333333&#038;s=0' alt='&#92;LaTeX' title='&#92;LaTeX' class='latex' /> file and recompile with C-c C-c, the PDF in the other window will automatically update.
</p>
<p>
This is achieved by placing the following line in my .emacs.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;" class="src src-emacs-lisp">
(add-hook 'doc-view-mode-hook 'auto-revert-mode)
</pre>
</div>
</div>
<div id="outline-container-1.3" class="outline-3">
<h3 id="sec-1.3">Screencast Example </h3>
<div id="text-1.3">
<p>
Here is a screencast of this process in action.
</p>
<span class='embed-youtube' style='text-align:center; display: block;'><iframe class='youtube-player' type='text/html' width='450' height='284' src='https://www.youtube.com/embed/BBzvlKtDFmQ?version=3&#038;rel=1&#038;fs=1&#038;showsearch=0&#038;showinfo=1&#038;iv_load_policy=1&#038;wmode=transparent' frameborder='0' allowfullscreen='true'></iframe></span>
<p>
This is a simple setup that I use to author reports, edit them, and see immediate updates to my output file without leaving Emacs.
</p>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/111/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/111/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=111&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
