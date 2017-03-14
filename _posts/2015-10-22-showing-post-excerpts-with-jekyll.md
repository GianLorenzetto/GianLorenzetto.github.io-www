---
layout: post
title: Showing post excerpts with Jekyll
categories: [www]
tags: [jekyll]
date: 2015-10-22 00:01:00
author: Gian Lorenzetto
---

I recently moved my blog to a [GitHub Pages](https://pages.github.com) site and based it on the nice [Hyde theme](https://github.com/poole/hyde) theme. One issue I had was that posts where not being truncated on the main index page. This is fine for shorter posts, but once you have a number of longer posts in the mix, scrolling down to find the next post is a real pain.

<!--more-->

There are a number of ways to do this, but the easiest is with the `post.excerpt` feature in Jekyll. To get this working I did the following:

1. Added `excerpt_separator: <!--more-->` to my `_config.yml`
    Optionally, you can add this to the top of each post, like so:
           
        ---
        layout: post
        title: Terminal replacement on Mac OS X
        excerpt_separator: <!--more-->
        ---

2. In the `index.html` file (or wherever you a listing your posts), you simply need to replace `post.content` with `post.excerpt`

Now, instead of the complete content of a post, you will only see everything before the `<!-- more -->` separator. 

Of course, for shorter posts, you can simply not include the `<!-- more -->` separator and the entire post will be displayed regardless.

The above works great, except that with the theme I was using the only way to see the complete post was to click on the title, which wasn't entirely obvious. So I added a `Read More ... ` link immediately after posts that were truncated.

Here's the complete code to optionally truncate on the `<!-- more -->` separator and then, if truncated, display a link to the complete post:

``` 
{% raw %}
{% if post.content contains site.excerpt_separator %}
    {{ post.excerpt }}
    <a href="{{ post.url }}"><strong>Read More ...</strong></a>
{% else %}
    {{ post.content }}
{% endif %}  
{% endraw %}
``` 

It's quite straight-forward.

- The first line

        {% raw %}{% if post.content contains site.excerpt_separator %}{% endraw %}

    just checks for the presence of the excerpt separator,
- if the separator is found, then only the excerpt is shown, along with the `Read More ...` link to the to full post (`post.url`),
- if the separator is not found, then the full post content is displayed.

And that's it!