---
title: "Making Emacs Buffer Names Unique Using the Uniquify Package"
kind: article
created_at: 2009-10-05 23:39:59 UTC
author: Blogistic Reflections
categories: 
tags: 
layout: post
---
<p>
If you ever work in Emacs with different files that all have the same name, this tip may be very useful for you.  In my experience, this most often happens when working with Makefiles from multiple projects or directories.  Assuming you have a buffer visiting a file called Makefile, by default Emacs will call the second buffer Makefile&lt;2&gt;. This is not very useful for figuring out which one is which.
</p>
<div id="outline-container-1.1" class="outline-3">
<h3 id="sec-1.1">The uniquify package </h3>
<div id="text-1.1">
<p>
Enter the <a href="http://www.emacswiki.org/emacs/uniquify">uniquify package</a>. It offers several options for making buffer names unique.  In my .emacs, I have the following two lines of code.
</p>
<pre style="background-color:#FFFFE5;font-size:8pt;" class="src src-emacs-lisp">
(<span style="color:#a020f0;font-weight:bold;">require</span> '<span style="color:#5f9ea0;">uniquify</span>)
(setq uniquify-buffer-name-style 'forward)
</pre>
<p>
You can set the value to any of the following options, nil being the default. These examples are taken from the help file within Emacs. They use the information from the directories the files are located in to make the names unique.  The first buffer called &#8220;name&#8221; is visiting a file in the directory bar/mumble/, and the second buffer is visiting a file called &#8220;name&#8221; in directory quux/mumble.
</p>
<table border="2" cellspacing="0" cellpadding="6" rules="groups">
<col align="left"></col>
<col align="left"></col>
<col align="left"></col>
<thead>
<tr>
<th>value</th>
<th>first buffer called &#8220;name&#8221;</th>
<th>second buffer called &#8220;name&#8221;</th>
</tr>
</thead>
<tbody>
<tr>
<td>forward</td>
<td>bar/mumble/name</td>
<td>quux/mumble/name</td>
</tr>
<tr>
<td>reverse</td>
<td>name\mumble\bar</td>
<td>name\mumble\quux</td>
</tr>
<tr>
<td>post-forward</td>
<td>name|bar/mumble</td>
<td>name|quux/mumble</td>
</tr>
<tr>
<td>post-forward-angle-brackets</td>
<td>name&lt;bar/mumble&gt;</td>
<td>name&lt;quux/mumble&gt;</td>
</tr>
<tr>
<td>nil</td>
<td>name</td>
<td>name&lt;2&gt;</td>
</tr>
</tbody>
</table>
</div>
</div><br />  <a rel="nofollow" href="http://feeds.wordpress.com/1.0/gocomments/blogisticreflections.wordpress.com/136/"><img alt="" border="0" src="http://feeds.wordpress.com/1.0/comments/blogisticreflections.wordpress.com/136/" /></a> <img alt="" border="0" src="https://pixel.wp.com/b.gif?host=blogisticreflections.wordpress.com&#038;blog=9541286&#038;post=136&#038;subd=blogisticreflections&#038;ref=&#038;feed=1" width="1" height="1" /><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Blogistic Reflections</a> - check out <a href="https://blogisticreflections.wordpress.com">Blogistic Reflections</a></i>
  </span>
</div>
