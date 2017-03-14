---
layout: post
title: Git Delete Local Merged Branches
categories: [development]
tags: [git]
date: 2016-07-14 14:26:00 +0800
author: Gian Lorenzetto
---

Every once in a while I like to clean up my local Git repo and remove all of the local branches that have been merged with a branch on the remote. Rather than doing this one branch at a time, here's a **PowerShell** one liner to do it for you (credit to [this SO answer](http://stackoverflow.com/questions/6127328/how-can-i-delete-all-git-branches-which-have-been-merged)).

```powershell
git branch --merged | ?{-not ($_ -like "*master")} | %{git branch -d $_.trim()}
```

<!--more-->

It's relatively safe, as it will explicitly ignore `master` and uses the little-_d_ delete and `--merged` options.

For the curious, that SO answer also contains a `bash` variant for those in _*nix_ consoles.