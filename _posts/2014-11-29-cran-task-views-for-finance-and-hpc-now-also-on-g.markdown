---
title: "CRAN Task Views for Finance and HPC now (also) on GitHub"
kind: article
created_at: 2014-11-29 02:14:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>The <a href="http://cran.r-project.org/web/views/">CRAN Task View</a> system is a fine project which <a href="http://eeecon.uibk.ac.at/~zeileis/">Achim Zeileis</a> initiated almost a decade ago. It is described in a short <a href="http://journal.r-project.org">R Journal</a> article in <a href="http://www.r-project.org/doc/Rnews/Rnews_2005-1.pdf">Volume 5, Number 1</a>. I have been editor / maintainer of the <a href="http://cran.r-project.org/web/views/Finance.html">Finance</a> task view essentially since the very beginning of these <a href="http://cran.r-project.org/web/views/">CRAN Task Views</a>, and added the <a href="http://cran.r-project.org/web/views/HighPerformanceComputing.html">High-Performance Computing</a> one in the fall of 2008. Many, many people have helped by sending suggestions or even patches; email continues to be the main venue for the changes.</p>
<p>The maintainers of the <a href="http://cran.r-project.org/web/views/WebTechnologies.html">Web Technologies</a> task view were, at least as far as I know, the first to make the jump to <a href="https://github.com/ropensci/webservices">maintaining the task view on GitHub</a>. <a href="http://karthik.io">Karthik</a> and I briefly talked about this when he was in town a few weeks ago for <a href="http://dirk.eddelbuettel.com/blog/2014/11/05#swc-at-nw-fall2014">our joint Software Carpentry workshop at Northwestern</a>.</p>
<p>So the topic had been on my mind, but it was only today that I realized that the near-limitless amount of awesome that is <a href="http://johnmacfarlane.net/pandoc/">pandoc</a> can probably help with maintenance. The task view code by <a href="http://eeecon.uibk.ac.at/~zeileis/">Achim</a> neatly converts the very regular, very XML, very boring original format into somewhat-CRAN-website-specific html. Pandoc, being as versatile as it is, can then make (GitHub-flavoured) markdown out of this, and with a minimal amount of <a href="http://en.wikipedia.org/wiki/Sed">sed</a> magic, we get what we need.</p>
<p>And hence we now have these two new repos:</p>
<ul>
<li><a href="https://github.com/eddelbuettel/ctv-finance">CRAN Task View for Finance, on GitHub</a></li>
<li><a href="https://github.com/eddelbuettel/ctv-hpc">CRAN Task View for High-Performance Computing with R, on GitHub</a></li>
</ul>
<p>Contributions are now most welcome by pull request. You can run the included converter scripts, it differs between both repos only by one constant for the task view / file name. As an illustration, the one for Finance is below.</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="co">#!/usr/bin/r</span>
## if you do not have /usr/bin/r from littler, just use Rscript

ctv &lt;-<span class="st"> &quot;Finance&quot;</span>

ctvfile  &lt;-<span class="st"> </span><span class="kw">paste0</span>(ctv, <span class="st">&quot;.ctv&quot;</span>)
htmlfile &lt;-<span class="st"> </span><span class="kw">paste0</span>(ctv, <span class="st">&quot;.html&quot;</span>)
mdfile   &lt;-<span class="st"> &quot;README.md&quot;</span>

## load packages
<span class="kw">suppressMessages</span>(<span class="kw">library</span>(XML))          <span class="co"># called by ctv</span>
<span class="kw">suppressMessages</span>(<span class="kw">library</span>(ctv))

r &lt;-<span class="st"> </span><span class="kw">getOption</span>(<span class="st">&quot;repos&quot;</span>)                 <span class="co"># set CRAN mirror</span>
r[<span class="st">&quot;CRAN&quot;</span>] &lt;-<span class="st"> &quot;http://cran.rstudio.com&quot;</span>
<span class="kw">options</span>(<span class="dt">repos=</span>r)

<span class="kw">check_ctv_packages</span>(ctvfile)             <span class="co"># run the check</span>

## create html file from ctv file
<span class="kw">ctv2html</span>(<span class="kw">read.ctv</span>(ctvfile), htmlfile)

### these look atrocious, but are pretty straight forward. read them one by one
###  - start from the htmlfile
cmd &lt;-<span class="st"> </span><span class="kw">paste0</span>(<span class="st">&quot;cat &quot;</span>, htmlfile,
###  - in lines of the form  ^&lt;a href=&quot;Word&quot;&gt;Word.html&lt;/a&gt;
###  - capture the &#39;Word&#39; and insert it into a larger URL containing an absolute reference to task view &#39;Word&#39;
  <span class="st">&quot; | sed -e &#39;s|^&lt;a href=</span><span class="ch">\&quot;\\</span><span class="st">([a-zA-Z]*</span><span class="ch">\\</span><span class="st">)</span><span class="ch">\\</span><span class="st">.html|&lt;a href=</span><span class="ch">\&quot;</span><span class="st">http://cran.rstudio.com/web/views/</span><span class="ch">\\</span><span class="st">1.html</span><span class="ch">\&quot;</span><span class="st">|&#39; | &quot;</span>,
###  - call pandoc, specifying html as input and github-flavoured markdown as output
              <span class="st">&quot;pandoc -s -r html -w markdown_github | &quot;</span>,
###  - deal with the header by removing extra ||, replacing |** with ** and **| with **:              
              <span class="st">&quot;sed -e&#39;s/||//g&#39; -e&#39;s/|</span><span class="ch">\\</span><span class="st">*</span><span class="ch">\\</span><span class="st">*/</span><span class="ch">\\</span><span class="st">*</span><span class="ch">\\</span><span class="st">*/g&#39; -e&#39;s/</span><span class="ch">\\</span><span class="st">*</span><span class="ch">\\</span><span class="st">*|/</span><span class="ch">\\</span><span class="st">*</span><span class="ch">\\</span><span class="st">* /g&#39; -e&#39;s/|$/  /g&#39; &quot;</span>,
###  - make the implicit URL to packages explicit
              <span class="st">&quot;-e&#39;s|../packages/|http://cran.rstudio.com/web/packages/|g&#39; &quot;</span>,
###  - write out mdfile
              <span class="st">&quot;&gt; &quot;</span>, mdfile)

<span class="kw">system</span>(cmd)                             <span class="co"># run the conversion</span>

<span class="kw">unlink</span>(htmlfile)                        <span class="co"># remove temporary html file</span>

<span class="kw">cat</span>(<span class="st">&quot;Done.</span><span class="ch">\n</span><span class="st">&quot;</span>)</code></pre>
<p>I am quite pleased with this setup---so a quick thanks towards the maintainers of the Web Technologies task view; of course to <a href="http://eeecon.uibk.ac.at/~zeileis/">Achim</a> for creating <a href="http://cran.r-project.org/web/views/">CRAN Task Views</a> in the first place, and maintaining them all those years; as always to <a href="http://johnmacfarlane.net/">John MacFarlance</a> for the magic that is <a href="http://johnmacfarlane.net/pandoc/">pandoc</a>; and last but not least <em>of course</em> to anybody who has contributed to the <a href="http://cran.r-project.org/web/views/">CRAN Task Views</a>.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
