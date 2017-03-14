---
layout: post
title: Git Branch Name Capitalisation
categories: [development]
tags: [git]
date: 2016-07-14 16:04:00 +0800
author: Gian Lorenzetto
---

I recently had an odd experience where Git was, seemingly randomly, changing the capitalisation of my branch names. This would happen when performing operations like changing branches and pushing branches.

tl;dr version, git stores branch prefixes like `Feature/` in a folder and file systems aren't case-sensitive. You need to delete the offending folder from `.git/refs/heads`. For a more detailed explanation, read on!

<!--more-->

It'll all started when I began using a branch naming scheme like `Feature/branch-name` and I thought that the `Feature` prefix may have been the issue ... and it kind of was, just not how I expected :)

After some googl'ing around I discovered that Git stores branches as files and more importantly, it treats branch names like `Foo/blah` as a _folder_ `Foo` within which there is a file `blah`.

... and file systems are not case-sensitive ...

Booh-yay!

Turns out I had accidently created a branch name `feature/something` at some time, and even though I had deleted the branch name, the folder lived on. Thus every time I created a new branch with the `Feature/` prefix, it would place it in the already existing `feature` (lower case) folder. While I was on the new branch, the prompt would be showing the upercase `Feature`, but when changing away from, and then back to, the branch it would see the lower case folder. Thus explaining the strange case change!

The fix is quite simple. Given a branch prefix `feature/` that you want to change to `Feature`, go to your Git repo, navigate to the

`../repo/.git/refs/heads`

folder and delete the `feature` folder (making sure it's empty of course).

The next time you create a branch `Feature/foo` there will be a new folder created with the correct capitalisation!
