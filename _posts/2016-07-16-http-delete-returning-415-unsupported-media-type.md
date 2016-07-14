---
layout: post
title: Http Delete Returning 415 Unsupported Media Type
categories: [development]
tags: [webapi]
date: 2016-07-14 16:18:00

---

When performing an HTTP Delete with a payload, WebAPI needs the content type to be specified, otherwise you're likely to see a `415 - Unsupported Media Type` response.

<!-- more -->

Here's a super simple delete request, with `content-type` included, for a JSON payload. Obviously, adjust the type to whatever your specific scenario requires. 

``` js
$http({
    method: 'DELETE',
    url: links.blah.href,
    headers: { 
        'Accept': 'application/vnd.hal+json',
        'Content-Type': 'application/json' }, // <---
    data: {
        dataNeededForDelete: someData
    }
});
```

