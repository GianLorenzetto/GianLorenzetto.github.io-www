---
layout: post
title: Azure TeamCity and OctopusDeploy
categories: []
tags: []

---

Recently, Mohamed Zaatar (a fellow Readifarian) and I spent some time creating a complete build and deployment pipeline. Our main goal was to create a fully functional CI server in Azure, with [TeamCity](TeamCity) for builds and [OctopusDeploy](https://octopus.com/) for deployments.

<!--more-->

Why? Firstly, although we both had some experience in parts of the technologies involved, neither of us had built a complete end-to-end environment, from scratch. Just sounded like too much fun!

Secondly, during my career as a software developer one of the things I've noticed is that many sites do not have a fully automated build and deployment environment. This just makes life incredible difficult, for a large number of reasons, including:

* builds are not repeatable,
* merging long lived feature branches becomes a nightmare,
* creating a release is often a manual and error prone exercise, and
deployment out to production is a cross-your-fingers, rollercoaster ride of disappointment.

This post will predominantly be about the key learnings we had while setting up the environment, while linking to some more detailed information. Note also that practically all of the steps below can be fully automated with PowerShell, but that's out of scope for this post.

### TL;DR

The executive level summary is to go read [this post by Andy French](http://www.andyfrench.info/2015/05/how-to-setup-teamcity-build-server-with.html). It's what we used as a guide and it provides great step-by-step instructions for getting a build server up and running (including Azure VM and TeamCity).

From there you just need to get Octopus installed and you're away!

Of course, there were a number of little (and not so little) issues we encountered along the way, which the rest of this post will cover.

Creating the Azure VM

Creating a VM on Azure is remarkably simple. The basic order of things is to:

1. Create a storage account with a SQL Server instance.
2. Create your VM

<div class="message">
<strong>Desktop or Server?</strong> Good question. My general thoughts here were that if you're application is designed to run on a desktop OS, then build/deploy on a desktop OS. However, Microsoft's licensing may have something to say about that. I imagine you're mileage will vary with this one, but there are a large number of pre-defined images to choose from, all pre-installed with VisualStudio and/or the build tools.
</div>

MORE DETAIL HERE, Resource Manager Vs Classic

If you followed along and took a look at the link above, you'll see that Andy created a Virtual Network, within which he created the VM. That's awesome if you want to have multiple machines all within a local subnet in Azure. For our purposes that was too complex, so we went done the stand-alone VM path.

<div class="message">
<strong>Note</strong> We've created a SQL Server database here for TeamCity. TeamCity itself can use most of the popular databases, but going the SQL route was simplest in this instance. Jump into the TeamCity docs to get a MySql or Postgresql installation rocking if that suits your needs.
</div>

A few things we learnt, in no particular order:

* When creating the DB, use a collation type ending in CS (e.g., something like XXXXX) - this forces case-sensitive sorting and filtering, which will make your TeamCity installation compatible with non-windows build agents.
* I really don't like the new portal - I found it more error prone than the classic view. It also didn't flow as nicely on my 13" MBP, but it might be a more pleasurable experience on a larger monitor.
* When you first create a VM, be sure to allocate some decent resources, at least multi-core and plenty of RAM. If you don't, your RDP sessions will drive you mad with the lag. It won't take long to configure (well, not if you follow this advice!) and you can down-grade the machine once your done.
* Be careful with your usernames and passwords. I got all 'secure' early on and created different named accounts with random passwords for just about everything and it was a bit of a nightmare to manage. Be secure. Just be a little pragmatic and don't go nuts.
* Don't forget to add exceptions for the various ports to your VM endpoints config, **but you must also add them to the VM OS firewall as well**. Yeah, that one didn't bite me ...
* Using the same name for your cloud service as for the VM can result in DNS clashes. This didn't seem to be a problem for us, but there were numerous posts about it online. Be warned.
* Save. Don't forget to save in the Azure management portal. What was that? Oh, did you forget to save? Save. Save. Save.

### TeamCity Installation

* Grab the latest NuGet and don't forget to enable the NuGet server.

#### OctoPack

OctopusDeploy requires a NuGet package to deploy. For that, we used OctoPack. OctoPack is a nifty little NuGet package that you can install into any deployable project (exe, lib, website). Once installed it automatically modifies the MSBuild script to create a NuGet package. Don't have a nuspec file? Doesn't matter, OctoPack creates one for you and does a good job of guessing what files are required based on the type of project (just make sure you at least review file for a real project!)

### OctopusDeploy installation

A couple of things to note:

* If you're using a non-standard port (say 8080) remember to open the port on the firewall of the server, as well as the endpoint configuration in the Azure management portal.
* Offline package drop creates the deployment, ready to be executed ... do NOT expect things like configuration variables to be substituted before running the deployment script.

#### Tentacles

Tentacles are quite straight-forward to install and represent a deployment target. Typically this will be another machine, possibly in a different environment (dev, test, prod).

* There are essentially two ways to configure a Tentacles: listening or polling. If at all possible it is recommend to use listening, as this is much less resource intensive. In polling mode the Tentacle will continuously poll the server for new packages to deploy. Listening mode will wait for a push from the Octopus server.
* Be careful when changing config to create a new Release to see changes, don't just change the process and re-deploy.