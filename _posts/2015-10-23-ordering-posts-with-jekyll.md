---
layout: post
title: Ordering posts with Jekyll
categories: []
tags: []

---

After switching to [GitHub Pages](https://pages.github.com) and [Jekyll](https://jekyllrb.com) for my blog, I ran into a problem wereby posts created on the same day where being ordered alphabetically, not in the order they where created. If you're like me, you don't post several blogs a day, so not really a major issue.

However, as I was moving some old posts across and using [Sublime Text](http://www.sublimetext.com) (with the [Jekyll package](https://packagecontrol.io/packages/Jekyll)) to create the new posts, it was using the current day in the post filenames. Long story short, I had a bunch of posts, all on the same day, no longer ordering corectly.

A quick google told me that you can add a `date:` field to the page front matter. For example:

```
---
layout: post
title: Ordering posts with Jekyll
date: 2015-10-23 09:06:59
---
```

Note that here, unlike the post filename, you can add the time as well! Problem solved. Just add the field to your posts and you can order them to your hearts content.

<div class="message"><strong>Note</strong> If you're using the awesome Sublime Text get yourself the Jekyll package and then all you need to do is open the `Command Palette` and select `Insert current datetime`. Here's a screen capture:</div>

![Sublime Text command palette]({{ site.url }}/images/ss_sublime_jekyll_currentdatetime.png "Sublime Text Command Palette showing Jekyll commands")

<div class="message"><strong>Note</strong> I considered adding the <code>date</code> property to the post template, but held off for a number of reasons:
<ol>
<li>I normally won't make more than one post a day, so it's just not a problem in general.</li>
<li>I typically start posts in the <code>_drafts/</code> folder, then move them across once I'm done. In this case, I really just want to set the <code>date</code> when I'm actually ready to publish the post. The command in the first note above makes that super easy and I'm quite happy with that workflow.</li>
</ol>
</div>