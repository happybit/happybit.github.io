---
layout: post
title: "Jekyll Notes"
date: 2014-07-03 19:17:08 +0800
comments: true
categories: Others
---

As I mentioned in [previous post](http://blog.pzheng.me/2014/05/25/migrating-from-octopress-to-jekyll/), Jekyll on GitHub is lack of some basic features such as category and archive pages since it doesn't support plugins. Here is how to add those features without plugin support. Of course, all tips were found from the open internet :smile:.

<!--more-->

## Footnotes

Sometimes we want to add some footnotes for reference as in [this post](http://blog.pzheng.me/2014/07/02/2014H1-summary/). The original markdown parser "redcarpet" cannot support it, at least for Jekyll on Github. We just need to change below line in `_config.yml`:

    markdown:         redcarpet

To:

    markdown:         kramdown

At the place you want to insert the subscript, just add `[^1]`. You can choose whatever number you like. Then at the end of post, add footnote as:

    [^1]: here is an example of footnote.

Please don't forget the colon mark next to `[^1]`.

## Disqus Comments

Insert below codes at the end of `_layouts/post.html`:

{% highlight html %}{% raw %}
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
{% endraw %}{% endhighlight %}

## Next/Previous Post Navigator

Insert below codes between `post` div and Disqus part in `_layouts/post.html`.

{% highlight html %}{% raw %}
<div class="navigator">
  {% if page.previous %}
      <span style="float:left"><a href="{{ page.previous.url }}">« {{ page.previous.title }}</a></span>
  {% endif %}
  {% if page.next %}
      <span style="float:right"><a href="{{ page.next.url }}">{{ page.next.title }} »</a></span>
  {% endif %}
</div>
{% endraw %}{% endhighlight %}

## Archive Page

Create new file `archive.html` in root directory as [this file](https://raw.githubusercontent.com/happybit/happybit.github.io/master/archive.html).

## Category Page

Create new file `categories.html` in root directory as [this file](https://raw.githubusercontent.com/happybit/happybit.github.io/master/categories.html).

You can display category for each post. Just need to add below line in `_layouts/post.html`:

{% highlight html %}{% raw %}
<span class="post-date">{{ page.date | date_to_string }}&nbsp;&nbsp;&nbsp;Category: {% for category in page.categories %}<a href="{{ site.url }}/categories.html#{{ category }}" title="Pages categorized {{ category }}" rel="category">{{ category }}</a>{% unless forloop.last %} &bull; {% endunless %}{% endfor %}</span>
{% endraw %}{% endhighlight %}

## Search & Feed

You can customize [Google](https://www.google.com/cse/all) search for your personal website. After get your specific URL, just paste into the appropriate place in `_includes/sidebar.html`:

    <a class="sidebar-nav-item" href="https://www.google.com:443/cse/publicurl?cx=xxxxxxxxxxxxx">Search</a>
	
Similarly, you can get the feed URL via [FeedBurner](www.feedburner.com).

    <a class="sidebar-nav-item" href="http://feeds.feedburner.com/knoise">RSS</a>

## Google Analytics

Create new file `_includes/google_analytics.html` and paste your Google Analytics scripts. Then insert below line before `<body>` in `_layouts/default.html`:

    {{ "{%" }}  include google_analytics.html %}

