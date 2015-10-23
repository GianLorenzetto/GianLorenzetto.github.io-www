---
layout: post
title: Moving to GitHub Pages
categories: []
tags: []
date: 2015-10-23 15:38:09
---

Having spent a few days with [GitHub Pages](https://pages.github.com), I thought I post some learnings in the hope they might help someome else moving to GitHub for blogging. I had a few hiccups at the start, but overall I'm really happy with how it's turned out.

Learnings -
* [Jekyll](https://jekyllrb.com) is pretty cool
  * has some really nice themes
  * not a lot of config, but that keeps it simple
  * [Liquid](http://liquidmarkup.org) is pretty straight-forward and it's easy to work with posts / draft etc
  * [Markdown](http://daringfireball.net/projects/markdown/) or Textile (actually uses [RedCloth](http://redcloth.org/hobix.com/textile/) for editing
  * Drop HTML straight into your Mardown for more advanced editing
  * Syntax hightlighting, with either [Liquid](http://liquidmarkup.org) or [GFM](https://help.github.com/articles/github-flavored-markdown/)
* Check the Jekyll documention - it's good and has lots of little tips to make life easier

A couple of other things I discovered-
* I don't like [Jekyll Boostrap](http://jekyllbootstrap.com) - I actually managed to start with this and nearly gave up on the whole [GitHub Pages](https://pages.github.com) adventure. Needless to say I had a lot of problems. Also appears that the project is dead.

# My workflow

My basic workflow goes someting like -
* Create draft (using [Sublime Text](http://www.sublimetext.com) with the [Jekyll package](https://packagecontrol.io/packages/Jekyll))
* Add any images in the post to my assests folder and push immediately to GitHub - this means I don't need to change the site `url` when running `Jekyll serve` locally (it'll pick them up from my GitHub.io page as for a published post, which is a nice check of the url as well). 
* Finsh the post and move to `_posts` folder (and don't forget to set the `date` in the front matter to prevent ordering issues, see [this post]({% post_url 2015-10-23-ordering-posts-with-jekyll %}))
* Push to GitHub

I also keep a file handy with a list of url's I use regularly, which you can see [here](https://github.com/GianLorenzetto/GianLorenzetto.github.io/blob/master/common_urls.md). Note that the file is in [Markdown](http://daringfireball.net/projects/markdown/), but I've used some `<pre></pre>` tags so that the file is useable both before and after formatting (ie, use locally or use from GitHub). 

