---
layout: post
title: Replacing the Windows console with Cmder
categories: [development]
tags: [terminal,windows]
date: 2015-10-23 17:39:41
author: Gian Lorenzetto
---

In a previous post I talked about [terminal replacements for Mac OS X]({% post_url 2015-10-22-terminal-replacement-on-mac-os-x %}). Unfortunately, on Windows the choices are less numerous.

<!--more-->

`PowerShell` is pretty awesome and on Windows 8/10 it quickly became my default environment, especially with [PosGit](https://github.com/dahlbyk/posh-git) installed. However, I was still looking for something ... more _*nix_'ish.

I tried [Babun](http://babun.github.io/), but I found the cygwin environment just foreign enough that I wasn't comfortable with it.

Enter [Cmder](http://cmder.net/). It’s based on [ConEmu](https://conemu.github.io/) but adds some nice Git and other configuration (make sure you grab the _msygit_ version). It also supports _tasks_, which allow you to quickly and easily create new tabs with, for example, an admin PowerShell, or a Git Bash terminal, or an admin chocolatey session.

Enjoy!