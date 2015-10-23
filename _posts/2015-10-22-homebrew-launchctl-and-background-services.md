---
layout: post
title: Homebrew, launchctl and background services
categories: [development, tools, mac]
tags: [cntlm, homebrew]

---

I installed `cntlm` on my MBP for a while as a proxy work-around on a client site and used `launchctl` to have it run the `cntlm` service at startup. Then I finished the gig and I wanted to prevent it from running … err, but I couldn’t find it using `launchctl list` or any other google supplied answer. Until I stumbled over [this blog](https://robots.thoughtbot.com/starting-and-stopping-background-services-with-homebrew).

<!--more-->

### tl;dr

1. Install brew services.

    `$ brew tap homebrew/services`

2. Find the pesky missing service.

    `$ brew services list`

The output consists of the `Name Status User Plist` and it's the last of these that we're intersted in:

<pre>
Name  Status  User Plist
cntlm started root <strong>/Library/../homebrew.mxcl.cntlm.plist</strong>
</pre>

Now just stop the service and remove the above plist file. That will prevent `cntlm` from running again in the future.