---
title: "Finance-YahooQuote 0.25 hotfix"
kind: article
created_at: 2015-04-29 12:59:00 UTC
author: Dirk Eddelbuettel
categories: 
tags: 
layout: post
---
<p>A hotfix release for the <a href="http://dirk.eddelbuettel.com/code/yahooquote.html">Finance-YahooQuote</a> Perl module on <a href="http://www.cpan.org/authors/id/E/ED/EDD/">CPAN</a> is now available. Available Yahoo! Finance decided to change the base URL. My thanks to <a href="http://www.physik.uzh.ch/~nchiapol/">Nicola Chiapolini</a> who not only noticed but also sent me the one-line patch fixing this:</p>
<pre class="pl"><code>--- YahooQuote.pm~      2010-03-27 01:44:10.000000000 +0100
+++ YahooQuote.pm       2015-04-29 11:31:20.407926674 +0200
@@ -34,7 +34,7 @@
 $VERSION = &#39;0.24&#39;;
 
 ## these variables govern what type of quote the modules is retrieving
-$QURLbase = &quot;http://download.finance.yahoo.com/d/quotes.csvr?e=.csv&amp;f=&quot;;
+$QURLbase = &quot;http://download.finance.yahoo.com/d/quotes.csv?e=.csv&amp;f=&quot;;
 $QURLformat = &quot;snl1d1t1c1p2va2bapomwerr1dyj1x&quot;;        # default up to 0.19
 $QURLextended = &quot;s7t8e7e8e9r6r7r5b4p6p5j4m3m4&quot;;        # new in 0.20
 $QURLrealtime = &quot;b2b3k2k1c6m2j3&quot;; # also new in 0.20</code></pre>
<p>If need be, edit your file <code>YahooQuote.pm</code> by hand.</p>
<p>This change in <a href="http://dirk.eddelbuettel.com/code/yahooquote.html">Finance-YahooQuote</a> will also affect <a href="http://dirk.eddelbuettel.com/code/beancounter.html">Beancounter</a> and <a href="http://dirk.eddelbuettel.com/code/beancounter.html">smtm</a> both of which use this module.</p>
<p>The fix has been pushed to <a href="http://www.debian.org">Debian</a> for the <a href="https://tracker.debian.org/pkg/finance-yahooquote">corresponding package</a> and to <a href="http://pause.perl.org/pause/query">PAUSE</a> for <a href="http://search.cpan.org/~edd/Finance-YahooQuote/YahooQuote.pm">CPAN package</a>.</p>
<p>Having maintained this since 2002 in RCS, I also just created a <a href="https://github.com/eddelbuettel/finance-yahooquote">GitHub repo</a> for it where development/maintenance will now happen.</p>
<p style="font-size:80%; font-style:italic;">
This post by <a href="http://dirk.eddelbuettel.com">Dirk Eddelbuettel</a> originated on his <a href="http://dirk.eddelbuettel.com/blog/">Thinking inside the box</a> blog. Please report excessive re-aggregation in third-party for-profit settings.
<p><div class="author">
  <img src="" style="width: 96px; height: 96;">
  <span style="position: absolute; padding: 32px 15px;">
    <i>Original post by <a href="http://twitter.com/">Dirk Eddelbuettel</a> - check out <a href="http://dirk.eddelbuettel.com/blog">Thinking inside the box   </a></i>
  </span>
</div>
