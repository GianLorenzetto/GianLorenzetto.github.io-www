---
layout: post
title: Git Push The Easy Way
categories: [development]
tags: [git]
date: 2016-07-14 13:55:00

---

Although I'm a big fan of [Git Extensions](https://gitextensions.github.io) on Windows, I still prefer the relative safety of the command line when doing things like pushing to the remote.

<!--more-->

Now normally, using say [PoshGit](https://github.com/dahlbyk/posh-git), I would type out something like

`> git push -u origin`

then cut/paste the branch name from the command prompt. Yes, I know that tab completion can be sort of a friend here, but often it's a little slow and the cut/paste can still be quicker. Either way, it's not a bad workflow.

But then I discovered that HEAD, as an alias to the current branch, works just as well as the branch name!

So just typing

`> git push -u origin HEAD`

works exactly as you'd expect - creating a remote branch with the current branch name!

Of course you can use it to do a normal push, fetch etc, wherever the current branch name is needed.

It doesn't help if you have a sudden case of _push-to-master-itis_, but still ... I think life changing isn't too much of a stretch for this one :)