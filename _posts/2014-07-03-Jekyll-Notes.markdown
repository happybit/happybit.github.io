---
layout: post
title: "Jekyll Notes"
date: 2014-07-03 19:17:08 +0800
comments: true
categories: Others
---

As I mentioned in [previous post](http://blog.pzheng.info/blog/2014/05/25/migrating-from-octopress-to-jekyll/), Jekyll on GitHub is lack of some basic features such as category and archive pages since it doesn't support plugins. Here is how to add those features without plugin support. Of course, all tips were found from the open internet :smilesmile:.

<!--more-->

## Footnotes

Sometimes we want to add some footnotes for reference as in [this post](http://blog.pzheng.info/blog/2014/07/02/2014H1-summary/). The original markdown parser "redcarpet" cannot support it, at least for Jekyll on Github. We just need to change below line in `_config.yml`:

    markdown:         redcarpet

To:

    markdown:         kramdown

At the place you want to insert the subscript, just add `[^1]`. You can choose whatever number you like. Then at the end of post, add footnote as:

    [^1]: here is an example of footnote.

Please don't forget the colon mark after `[^1]`.

## Disqus Comments

Insert below codes at the end of `_layout/post.html`:

    <div id="disqus_thread"></div>
    <script type="text/javascript">
        /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
        var disqus_shortname = 'YOURNAME'; // required: replace example with your forum shortname
    
        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
            var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
            dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
            (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>

## Next/Previous Post Navigator

Insert below codes between `post` div and Disqus part in `_layout/post.html`.

    <div class="navigator">
      {% if page.previous %}
          <span style="float:left"><a href="{{ page.previous.url }}">« {{ page.previous.title }}</a></span>
      {% endif %}
      {% if page.next %}
          <span style="float:right"><a href="{{ page.next.url }}">{{ page.next.title }} »</a></span>
      {% endif %}
    </div>

## Archive Page



## Category Page
