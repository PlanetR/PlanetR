---
title: "RcppTOML 0.0.3: A New Approach to Configuration Files"
kind: article
created_at: 2015-04-29 01:43:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A small project I worked on during the last few weeks has now come together in new package <a href="http://dirk.eddelbuettel.com/code/rcpp.toml.html">RcppTOML</a> which arrived on <a href="http://www.r-project.org">CRAN</a> yesterday.</p>
<p>It provides <a href="http://www.r-project.org">R</a> with a reader for <em>TOML</em> files. TOML stands for <em>Tom's Obvious Markup Language</em>. And before you roll your eyes, glance at the <a href="https://github.com/toml-lang/toml">TOML site</a>. It really is different, and has a number of rather wonderful features:</p>
<ul>
<li>free-format indentation as you please</li>
<li>comments anywhere, even on the same line</li>
<li>actual <em>types</em> such as string, integer, float, bool and datetime (!!) which are all native</li>
<li>vectors, of course, of the above</li>
<li>arbitrary nesting of tables</li>
</ul>
<p>Here is a simple illustration where we parse the <a href="https://github.com/eddelbuettel/rcpptoml/blob/master/inst/toml/example.toml">TOML example file</a> derived from what is part of the main <a href="https://github.com/toml-lang/toml">TOML README</a></p>
<pre class="sourceCode r"><code class="sourceCode r">R&gt;<span class="st"> </span>p &lt;-<span class="st"> </span><span class="kw">parseTOML</span>(<span class="kw">system.file</span>(<span class="st">&quot;toml&quot;</span>, <span class="st">&quot;example.toml&quot;</span>, <span class="dt">package=</span><span class="st">&quot;RcppTOML&quot;</span>))
R&gt;<span class="st"> </span><span class="kw">summary</span>(p)
toml object with top-level slots:
<span class="st">   </span>clients, database, owner, servers, title 
read from /usr/local/lib/R/site-library/RcppTOML/toml/example.toml 
R&gt;<span class="st"> </span>p
List of <span class="dv">5</span>
 $<span class="st"> </span>clients :List of <span class="dv">2</span>
  ..$<span class="st"> </span>data :List of <span class="dv">2</span>
  .. ..$<span class="st"> </span><span class="er">:</span><span class="st"> </span>chr [<span class="dv">1</span>:<span class="dv">2</span>] <span class="st">&quot;gamma&quot;</span> <span class="st">&quot;delta&quot;</span>
  .. ..$<span class="st"> </span><span class="er">:</span><span class="st"> </span>int [<span class="dv">1</span>:<span class="dv">2</span>] <span class="dv">1</span> <span class="dv">2</span>
  ..$<span class="st"> </span>hosts:<span class="st"> </span>chr [<span class="dv">1</span>:<span class="dv">2</span>] <span class="st">&quot;alpha&quot;</span> <span class="st">&quot;omega&quot;</span>
 $<span class="st"> </span>database:List of <span class="dv">4</span>
  ..$<span class="st"> </span>connection_max:<span class="st"> </span>int <span class="dv">5000</span>
  ..$<span class="st"> </span>enabled       :<span class="st"> </span>logi <span class="ot">TRUE</span>
  ..$<span class="st"> </span>ports         :<span class="st"> </span>int [<span class="dv">1</span>:<span class="dv">3</span>] <span class="dv">8001</span> <span class="dv">8001</span> <span class="dv">8002</span>
  ..$<span class="st"> </span>server        :<span class="st"> </span>chr <span class="st">&quot;192.168.1.1&quot;</span>
 $<span class="st"> </span>owner   :List of <span class="dv">4</span>
  ..$<span class="st"> </span>bio         :<span class="st"> </span>chr <span class="st">&quot;GitHub Cofounder &amp; CEO</span><span class="ch">\\</span><span class="st">nLikes tater tots and beer.&quot;</span>
  ..$<span class="st"> </span>dob         :<span class="st"> </span>POSIXct[<span class="dv">1</span>:<span class="dv">1</span>], format:<span class="st"> &quot;1979-05-27 07:32:00&quot;</span>
  ..$<span class="st"> </span>name        :<span class="st"> </span>chr <span class="st">&quot;Tom Preston-Werner&quot;</span>
  ..$<span class="st"> </span>organization:<span class="st"> </span>chr <span class="st">&quot;GitHub&quot;</span>
 $<span class="st"> </span>servers :List of <span class="dv">2</span>
  ..$<span class="st"> </span>alpha:List of <span class="dv">2</span>
  .. ..$<span class="st"> </span>dc:<span class="st"> </span>chr <span class="st">&quot;eqdc10&quot;</span>
  .. ..$<span class="st"> </span>ip:<span class="st"> </span>chr <span class="st">&quot;10.0.0.1&quot;</span>
  ..$<span class="st"> </span>beta :List of <span class="dv">2</span>
  .. ..$<span class="st"> </span>dc:<span class="st"> </span>chr <span class="st">&quot;eqdc10&quot;</span>
  .. ..$<span class="st"> </span>ip:<span class="st"> </span>chr <span class="st">&quot;10.0.0.2&quot;</span>
 $<span class="st"> </span>title   :<span class="st"> </span>chr <span class="st">&quot;TOML Example&quot;</span>
<span class="ot">NULL</span>
R&gt;<span class="st"> </span></code></pre>
<p>See much more at the <a href="https://github.com/toml-lang/toml">TOML</a> site. I converted one first project at work to this and it really rocks. Point to a file, get a list back and index all components by their names.</p>
<p>We also added really simple S3 classes to the default <code>print()</code> method uses <code>str()</code> for a more compact presentation of what (in R) is of course nested list types.</p>
<p>Internally, the <a href="http://dirk.eddelbuettel.com/code/rcpp.toml.html">RcppTOML</a> packages use the splendid <a href="https://github.com/skystrife/cpptoml">cpptoml</a> parser by Chase Geigle. This brings in modern C++11 and makes it that <a href="http://www.r-project.org">CRAN</a> simply cannot build a binary for R on Windows as the g++ version (still, as of April 2015) in Rtools is too old. There is word of an update to Rtools and that point should we able to support Windows as well. Until then, no mas.</p>
<p>A bit more information is on the <a href="http://dirk.eddelbuettel.com/code/rcpp.toml.html">package page here</a> as well as as the <a href="https://github.com/eddelbuettel/rcpptoml">GitHub repo</a>.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
