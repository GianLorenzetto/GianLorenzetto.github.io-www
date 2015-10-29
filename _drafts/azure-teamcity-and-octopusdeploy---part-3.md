---
layout: post
title: Azure, TeamCity and OctopusDeploy - Part 3
categories: []
tags: []

---

This is Part 3 of Mohamed (https://twitter.com/mzaatar) and Gian's adventures in setting up a CI and deployment pipeline. [Part 1 XXX](TODO) covered creating a VM in Azure and [Part 2 XXX](TODO) discussed installing TeamCity. Go do them and then come back ... done? Then let's more on!

[OctopusDeploy](http://octopus.com) does one thing, but it does it really, really well: deployments (surprise!).

It's almost trivial to install and configure, but there where a few little things I didn't know when we started this:

1. OctopusDeploy needs [NuGet](https://www.nuget.org) packages - everything you deploy will need to be NuGet-packaged. If you're not familiar with NuGet packaging you'll want to pay attention to the OctoPack section below.
2. OctopusDeploy uses the concept of a central server and deployment targets, called _tentacles_.

The rest of this post is organised as follows:

1. [Installing OctopusDeploy](#installing-octopus)
2. [Installing Tentacles](#installing-tentacles)
3. [Setting up Environments](#octopus-setup)
4. [Variable Substitution](#variable-substitution)
5. [Packaging with OctoPack](#octopack)

<a name="installing-octopus"></a>
### Installing OctopusDeploy

A couple of things to note:

* If you're using a non-standard port (say 8080) remember to open the port on the firewall of the server, as well as the endpoint configuration in Azure management portal.
* Offline package drop creates the deployment, ready to be executed ... do NOT expect things like configuration variables to be substituted before running the deployment script.

<a name="installing-tentacles"></a>
### Installing Tentacles

Tentacles are quite straight-forward to install and represent a deployment target. Typically this will be another machine, possibly in a different environment (dev, test, prod).

* There are essentially two ways to configure a Tentacles: listening or polling. If at all possible it is recommend to use listening, as this is much less resource intensive. In polling mode the Tentacle will continuously poll the server for new packages to deploy. Listening mode will wait for a push from the Octopus server.
* Be careful when changing config to create a new Release to see changes, don't just change the process and re-deploy.

<a name="octopus-setup"></a>
### Setting up Environments

OctopusDeploy uses the concept of _Environments_ to define different deployment targets. These might be _DEV_, _PROD_ or _TEST_. Within an Environment you must define a deployment target - essentially a machine to which a package will be deployed.

<a name="Variable Substition"></a>
### Variable Substitution

One of the simplest, but easily one of the most useful, features of OctopusDeploy is it's ability to perform variable substitution, based on the target Environment.

For `*.config` files it can be as simple as specifying the variable in OctopusDeploy and it will automatically hunt through all the `*.confg` files in your app and replace those with a `key` matching the variable name.

There are alos more complex transformations available, useful for defining a common `.confg` and partial versions for different configurations (Release, Debug).

<a name="octopack"></a>
### Packaging with OctoPack

OctopusDeploy requires a NuGet package to deploy. For that, we used OctoPack. OctoPack is a nifty little NuGet package that you can install into any deployable project (exe, lib, website). Once installed it automatically modifies the MSBuild script to create a NuGet package. Don't have a nuspec file ( what is nsupec file - needs clarification) ? Doesn't matter, OctoPack creates one for you and does a good job of guessing what files are required based on the type of project (just make sure you at least review file for a real project!)
