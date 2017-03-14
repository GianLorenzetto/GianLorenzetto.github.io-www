---
layout: post
title: WebAPI Wildcard In Route
categories: [development]
tags: [webapi]
date: 2016-07-14 19:44:00 +0800
author: Gian Lorenzetto
---

I recently discovered that it's possible to include a wildcard (the `*` character) in a WebApi route. It looks something like:

```csharp
[Route(some/route/{*key})]
```

<!--more-->

[This ASP.Net article](http://www.asp.net/web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing) has a good example (search for the 'wildcard' section).

Essentially, everything beyond the `route/` part of the url will be assigned to the `key` variable. For example, the route

`some/route/more/parts/here?param=1`

results in 

```csharp
key = "more/parts/here?param=1";
```

This can be useful for things like file storage and other uri params that may include folder paths or similar.