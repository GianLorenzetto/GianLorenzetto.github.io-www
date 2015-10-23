---
layout: post
title: Azure, TeamCity and OctopusDeploy - Part 2
categories: []
tags: []

---

This is Part 2 in ... In Part 1 ...

### TeamCity Installation

* Grab the latest NuGet and don't forget to enable the NuGet server.

#### OctoPack

OctopusDeploy requires a NuGet package to deploy. For that, we used OctoPack. OctoPack is a nifty little NuGet package that you can install into any deployable project (exe, lib, website). Once installed it automatically modifies the MSBuild script to create a NuGet package. Don't have a nuspec file? Doesn't matter, OctoPack creates one for you and does a good job of guessing what files are required based on the type of project (just make sure you at least review file for a real project!)