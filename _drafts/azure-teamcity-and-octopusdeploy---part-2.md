---
layout: post
title: Azure, TeamCity and OctopusDeploy - Part 2
categories: []
tags: []

---

This is Part 2 of [Mohamed](https://twitter.com/mzaatar) and Gian's adventures in creating a complete CI and deployment pipeline. If you missed it, [Part 1 XXXX](TODO) was all about setting up a suitable VM in Azure. If you haven't already done so, what are you waiting for!

In this post, I'll cover how we installed and configured TeamCity.

### TeamCity Installation

Installing TeamCity is a really straight-forward process.

1. [Grab the latest installer.](#get-installer) 
2. [Run the installer on the VM.](#install-teamcity)
3. [Perform some basic initial configuration.](#initial-config)

Let's go into the above in a little mote detail.

<a name="get-installer"></a>
### TeamCity Download

Grabbing the latest installer is pretty easy. You can obviously do this directly from the VM, or just upload from another location. Either way you just need to get the installer onto the VM :)

I had some security issues with IE on Server 2012 R2. Just use [Chrome](https://www.google.com/chrome/).

<a name="install-teamcity"></a>
### Running the Installer

Running the installer is super easy. Obviously you can modify the defaults as you wish, but all the settings obvious in their purpose.

You will need to go to the MS downloads site and grab the latest Java ODBC SQL Server library (www link)(TODO) , helpfully pointed out as part of the TeamCity installation:

<a name="initial-config"></a>
### Initial Configuration

#### Setup NuGet

You'll almost certainly want to get NuGet setup and running in TeamCity.

* Get the latest NuGet
* Enable the TeamCity NuGet server.

You must enable the NuGet Server for TeamCity to be able work correctly with NuGet feeds.

### Nuget Feeds

TeamCity has an awesome feature I only discovered recently - it supports NuGet feeds out-of-the-box. Not just that, all  you need to to is push a new branch, ad TeamCity will automatically create a feed for you at:

`{your_package_name}{version}{branch_id}`

Note that the `{branch_id}` is just a truncated form of the branch name. This feature makes testing out NuGet deployed libraries an absolute breeze!