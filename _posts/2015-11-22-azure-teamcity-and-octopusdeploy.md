---
layout: post
title: Azure, TeamCity and OctopusDeploy - Part 1
categories: [Development]
tags: [Azure,TeamCity,OctopusDeploy,CI]
date: 2015-11-22 08:44:37
author: Gian Lorenzetto
---

Recently, [Mohamed](https://twitter.com/mzaatar) (a fellow Readifarian) and I spent some time creating a complete build and deployment pipeline. Our main goal was to create a fully functional [CI](https://www.thoughtworks.com/continuous-integration) server in Azure, with [TeamCity](https://www.jetbrains.com/teamcity/) for builds and [OctopusDeploy](https://octopus.com/) for deployments.

<!--more-->

Why? Firstly, although we both had some experience in parts of the technologies involved, neither of us had built a complete end-to-end environment, from scratch. Just sounded like too much fun!

Secondly, during my career as a software developer one of the things I've noticed is that many sites do not have a fully automated build and deployment environment. This just makes life incredible difficult, for a large number of reasons, including:

* builds are not repeatable,
* merging long lived feature branches becomes a nightmare,
* creating a release is often a manual and error prone exercise, and
* deployment out to production is a cross-your-fingers, roller-coaster ride of disappointment.

This post includes:

* the key learnings we had while setting up the environment, and
* links to some more detailed information we found useful.

This post won't include:

* detailed step-by-step instructions on setting up Azure, TeamCity and OctopusDeploy (there are plenty of those, see below), or
* automation with PowerShell (that's for another post!).

## tl;dr

The executive level summary is to go read [this post by Andy French](http://www.andyfrench.info/2015/05/how-to-setup-teamcity-build-server-with.html). It's what we used as a guide and it provides great step-by-step instructions for getting a build server up and running (including Azure VM and TeamCity).

From there you just need to get Octopus installed and you're away!

Of course, there were a number of little (and not so little) issues we encountered along the way, which the rest of this post will cover.

## Creating the Azure VM

Creating a VM on Azure is remarkably simple. The basic order of things is to:

1. [Create a Virtual Network](#step1)
2. [Create a Storage Account](#step2-3)
3. [Create a SQL Server DB](#step2-3)
4. [Create a Cloud Service](#step4)
5. [Create a Virtual Machine](#step5)

<a name="step1"></a>
### Step 1 - Virtual Network

For our needs, setting up a _Virtual Network_ was overkill, thus we skipped this step. However, if you would like to setup a multi-machine environment on the one sub-net in Azure, then you will need to do this. For us the stand-alone VM option was perfectly suitable.

<a name="step2-3"></a>
### Step 2,3 - Storage and Database

Steps 2 and 3 are optional. A _Storage Account_ will be automatically created for you when you create the VM if you don't already have one defined.

As we're using TeamCity, we chose to create a Azure SQL Server DB. TeamCity has it's own, built-in database (HSQLDB), which you could use as a trial, but it's not for anything else. From the [TeamCity documentation](https://confluence.jetbrains.com/display/TCD8/Setting+up+an+External+Database):

>The internal database may crash and lose all your data (e.g. on out of disk space condition). Also, internal database can become extremely slow on large data sets (say, database storage files over 200Mb). Please also note that our support does not cover any performance or database data loss issues if you are using the internal database.  
In short, **do not EVER use internal HSQLDB database for production TeamCity instances**. 

Note that the emphasis above is from the TeamCity doco, not mine.

Lastly, if you're going to be using TeamCity for non-Windows builds, it's strongly recommended to select a _collation_ type ending in 'CS_AS'. From the [TeamCity SQL Server documentation](https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database#SettingupanExternalDatabase-MicrosoftSQLServer):

>As the primary collation, it is recommended to use the collation corresponding to your locale. We also suggest using the case-sensitive collation (collation name ending with 'CS_AS'), which is mandatory for the certain functionality (like using non-Windows build agents). 

And here's a screen capture of that setting in the classic portal:

![SQL Server collation setting]({{ site.url }}/images/ss_sqldb_collation_type.png "SQL Server collation setting")

And here's what the setting looks like in the preview portal:

![SQL Server collation setting]({{ site.url }}/images/ss_sqldb_collation_type_previewportal.png "SQL Server collation setting")

<div class="message">
<strong>Note</strong> We created a SQL Server database for TeamCity, but it can use most of the popular databases. Going the SQL Server route was simplest in this instance, however <a href="https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database">jump into the TeamCity docs</a> to get a <a href="https://www.mysql.com">MySql</a> or <a href="http://www.postgresql.org">PostgreSQL</a> installation rocking if that suits your needs.
</div>

<a name="step4"></a>
### Step 4 - Cloud Service

A [Cloud Service](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-choose-me/) is a (Azure processing unit) container for one or more virtual machines, giving you the ability to load balance your service. The image below is from the linked Cloud Services article above and gives a brief description of the different hosting models for you application:

![Azure Hosting Models]({{ site.url }}/images/ss_azure_hostingmodelstable.png "The three different hosting models in Azure")

In this instance, we wanted to create our own VM, but we did not need the added features (and complexity) of the Cloud Services model. Azure makes this easy, as when you create the VM you can either:
- select an existing Cloud Service, or
- one will be automatically created for you.

We took the latter option.

Also note that Azure will automatically name the Cloud Service with the same name as the VM, which means they will have the same DNS name (eg, the service and the VM will both be at `myvm.cloudapp.net`). There were some articles on SO that indicated this may be a problem, but we never had an issue (except for when I forget to open the appropriate ports on the VM's local firewall, but that's another story ...). In more complex, multi-VM environments this may be something to consider.

<a name="step5"></a>
### Step 5 - Creating the Virtual Machine

When creating a VM, you really just need to select:

* an image name, 
* a name for the machine,
* the tier and size, and
* the region.

If you're going for a build server, as we were, when selecting the image name be sure to pick one _with VisualStudio installed_ ... perhaps too much coffee that day. In the end we had success with both `Windows Server 2012` and `Windows 10` VM's.

The easiest way to do this is to go to the Azure Marketplace:

![Selecting an image]({{ site.url }}/images/ss_azure_imagemarketplace.png "Selecting an image with Visual Studio installed")

Then just enter '_Visual Studio_' in the filter at the top of the page. Note that you may only see entries for Visual Studio _2013_ in the drop-down:

![Azure Marketplace]({{ site.url }}/images/ss_azure_imagemarketplace_vs2013only.png "Azure Marketplace for selecting an image")

Just hit `Enter` in filter box and wait for the full list to display. From there just pick the edition and release that suits your needs:

![Selecting a VM image]({{ site.url }}/images/ss_azure_imagemarketplace_vsfulllisting.png "Selecting and image name including Visual Studio")

<div class="message">
<strong>Desktop Image or Server?</strong> Good question. My general thoughts here were that if your application is designed to run on a desktop OS, then build/deploy on a desktop OS. However, Microsoft's licensing may have something to say about that. I imagine your mileage will vary with this one, but there is a large number of pre-defined images to choose from, all pre-installed with VisualStudio and/or the build tools.
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

* We both started with the the new management portal (https://portal.azure.com), but switched back to the classic view (https://manage.windowsazure.com). In general, I found the new portal a little less friendly than the classic view. It also didn't flow as nicely on my 13" MBP, but it might be a more pleasurable experience on a larger monitor.
* Be careful with your _usernames_ and _passwords_. I got all 'secure' early on and created different named accounts with random passwords for just about everything and it was a bit of a nightmare to manage. Be secure. Just be a little pragmatic and don't go nuts.
* Save. Don't forget to save in the Azure management portal. What was that? Oh, did you forget to save? Save. Save. Save.

## Conclusion

Hope that was useful. Coming up in Part 2 is TeamCity installation and setup.