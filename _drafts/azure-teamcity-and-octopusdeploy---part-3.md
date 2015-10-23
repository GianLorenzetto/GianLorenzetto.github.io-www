---
layout: post
title: Azure, TeamCity and OctopusDeploy - Part 3
categories: []
tags: []

---

This is Part 3 in ... In Part 1 ... and in Part 2 ...

### OctopusDeploy installation

A couple of things to note:

* If you're using a non-standard port (say 8080) remember to open the port on the firewall of the server, as well as the endpoint configuration in the Azure management portal.
* Offline package drop creates the deployment, ready to be executed ... do NOT expect things like configuration variables to be substituted before running the deployment script.

#### Tentacles

Tentacles are quite straight-forward to install and represent a deployment target. Typically this will be another machine, possibly in a different environment (dev, test, prod).

* There are essentially two ways to configure a Tentacles: listening or polling. If at all possible it is recommend to use listening, as this is much less resource intensive. In polling mode the Tentacle will continuously poll the server for new packages to deploy. Listening mode will wait for a push from the Octopus server.
* Be careful when changing config to create a new Release to see changes, don't just change the process and re-deploy.