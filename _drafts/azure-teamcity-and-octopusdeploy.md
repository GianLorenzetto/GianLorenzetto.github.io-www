---
layout: post
title: Azure, TeamCity and OctopusDeploy - Part 1
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
* deployment out to production is a cross-your-fingers, rollercoaster ride of disappointment.

This post will predominantly be about the key learnings we had while setting up the environment, while linking to some more detailed information. Note also that practically all of the steps below can be fully automated with PowerShell, but that's out of scope for this post.

## TL;DR

The executive level summary is to go read [this post by Andy French](http://www.andyfrench.info/2015/05/how-to-setup-teamcity-build-server-with.html). It's what we used as a guide and it provides great step-by-step instructions for getting a build server up and running (including Azure VM and TeamCity).

From there you just need to get Octopus installed and you're away!

Of course, there were a number of little (and not so little) issues we encountered along the way, which the rest of this post will cover.

## Creating the Azure VM

Creating a VM on Azure is remarkably simple. The basic order of things is to:

1. Create a Virtual Network.
2. Create a Storage Account.
3. Create a SQL Server DB.
4. Create a Cloud Service.
5. Create a Virtual Machine.

### Step 1 - Virtual Network

Step 1 was overkill for us and so we skipped it. But essentially, if you would like to setup a multi-machine enviroment, go for it. For us the stand-alone VM option was fine.

### Step 2,3 - Storage

Steps 1, 2 are optional. A Storage Account will be automatically created for you when you create the VM if you don't already have one defined.

As we're using TeamCity, we chose to create a SQL Server DB. TeamCity has it's own, built-in database (HSQLDB), which you could use as a trial, but it's not for anything else. From the [TeamCity documentation](https://confluence.jetbrains.com/display/TCD8/Setting+up+an+External+Database):

>The internal database may crash and lose all your data (e.g. on out of disk space condition). Also, internal database can become extremely slow on large data sets (say, database storage files over 200Mb). Please also note that our support does not cover any performance or database data loss issues if you are using the internal database.  
In short, **do not EVER use internal HSQLDB database for production TeamCity instances**. 

Note that the emphasis above is from the TeamCity doco, not mine.

Lastly, if you're going to be using TeamCity for non-Windows builds, it's strongly recommended to select a _collation_ type ending in 'CS_AS'. From the [TeamCity SQL Server documentation](https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database#SettingupanExternalDatabase-MicrosoftSQLServer):

>As the primary collation, it is recommended to use the collation corresponding to your locale. We also suggest using the case-sensitive collation (collation name ending with 'CS_AS'), which is mandatory for the certain functionality (like using non-Windows build agents). 

And here's a screen capture of that setting in the classic portal:

![SQL Server collation setting]({{ site.url }}/images/ss_sqldb_collation_type.png "SQL Server collation setting")

<div class="message">
<strong>Note</strong> We've created a SQL Server database here for TeamCity, but it can use most of the popular databases. Going the SQL route was simplest in this instance, however jump into the TeamCity docs to get a MySql or Postgresql installation rocking if that suits your needs.
</div>

### Step 4 - Cloud Service

A Cloud Service is a container for one or more virtual machines, giving you the ability to load balance your service. Again, this was too complex for our needs and a Cloud Service will be automatically created for you. 

Note that Azure will automatically name the cloud service with the same name as the VM, which means they will have the same DNS name (eg, the service and the VM will both be at `myvm.cloudapp.net`). There were some articles on SO that indicated this may be a problem, but we never had an issue (except for when I forget to set the firewall up correctly on the VM, but that's another story ...). In more complex, multi-VM environments this may be something to consider.

### Step 5 - Virtual Machine

When creating a VM, you really just need to select:

* an image name, 
* a name for the machine,
* the tier and size, and
* the region.

If you're going for a build server, as we were, when selecting the image name be sure to pick one _with VisualStudio installed_ ... perhaps too much coffee that day. In the end I had success with both Windows Server 2012 and Windows 10 VM's.

<div class="message">
<strong>Desktop Image or Server?</strong> Good question. My general thoughts here were that if you're application is designed to run on a desktop OS, then build/deploy on a desktop OS. However, Microsoft's licensing may have something to say about that. I imagine you're mileage will vary with this one, but there are a large number of pre-defined images to choose from, all pre-installed with VisualStudio and/or the build tools.
</div>

Also, when you first create a VM be sure to allocate some decent resources, at least multi-core and plenty of RAM. If you don't, your RDP sessions will drive you mad with the lag. It won't take long to configure (well, not if you follow this advice!) and you can down-grade the machine once your done.

There is also an option to select an _Availability Set_. I believe this allows you to configure fail-over into other regions / data centres, but for our purposes we just selected the default of _'(None)'_.

If you're using the new Azure management portal, you will also see an option for the _Deployment Model_. This option is not available in the classic view and allows you to select:

* **Classic** (also known as _Service Managed_) and is the same as using the old portal, or
* **Resource Managed** this is a new option, allowing deployment of groups of resources as a single entity.

Here's what it looks like in the new portal:

![Deployment Model setting]({{ site.url }}/images/ss_azurepreviewportal_deploymentmodel.png "Deployment Model setting")

Follow the link to more detail on the [differences between _Resource_ and _Service Managed_ deployment models](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/). Note that they are not entirely compatible. From the article:

>The Resource Manager deployment model provides a new way to deploy and manage the services that make up your application. This new model contains important differences from the classic deployment model, and the two models are not completely compatible with each other. To simplify the deployment and management of resources, Microsoft recommends that you use Resource Manager for new resources, and, if possible, re-deploy existing resources through Resource Manager. 

Lastly, be sure to update the _Endpoints_ configuration to add any port exceptions you may need (this was especially true for OctopusDeploy, which we put at the non-standard port 8080). This can be done when you create the VM as well as later on in the configuration settings.

<div class="message">
<strong>Gotcha</strong> Don't forget to add exceptions for the various ports to your VM Endpoints config, <em>but you must also add them to the VM OS firewall as well</em>. Yeah, that one didn't bite me ...
</div>

## Learnings

A few other miscellaneous things we learnt, in no particular order:

* I started off using the new portal, then switched back to the classic view. In general, I found the new portal a little more error prone than the classic view. It also didn't flow as nicely on my 13" MBP, but it might be a more pleasurable experience on a larger monitor.
* Be careful with your usernames and passwords. I got all 'secure' early on and created different named accounts with random passwords for just about everything and it was a bit of a nightmare to manage. Be secure. Just be a little pragmatic and don't go nuts.
* Save. Don't forget to save in the Azure management portal. What was that? Oh, did you forget to save? Save. Save. Save.

## Conclusion

Hope that was useful. Coming up in Part 2 is TeamCity installation and setup.