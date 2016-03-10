---
layout: post
title: APIDays 2016 Highlights
categories: [Conference]
tags: [APIDays]
date: 2016-03-10 12:40:00
---

My notes and highlights from [APIDays](http://au.apidays.io) 2016 in Melbourne.

Slides are available for most presentations and are linked to from the abstract pages for each talk. You can get to the abstracts by clicking through the links to each individual talk in the [program](http://au.apidays.io/#program).

<!--more-->

# [Steve Sammartino - Welcome to Startup Land](http://au.apidays.io/slides/sammartino-startup-land.pdf)

This was the first keynote on day one and kicked things off with some interesting thinking around innovation, what it is, what it means and how it can challenge older / larger organisations who have operated in the same way for a long time. 

He discussed how companies, in the context of innovation, should embrace _horizontal thinking_. The example being that of Fosters, a large brewing company and that they should be investing heavily in auto-driving cars :) Pretty funny, but also pretty savvy and set the tone for a number of examples of how innovation can come about through the connection of devices we never would have considered.

Another example was that of the connected toilet! Imagine a toilet that actually took your blood pressure, blood glucose levels, heart rate, dietary contents (ewww) and so on and fed that to your doctor! It's a pretty brutal invasion of privacy (my first thought) but if it means that your doctor can catch cancer and tell you before you even notice any symptoms then that might just be worth it? ...

On APIs themselves, he stressed that you shouldn't be afraid of selling an unfinished product, as this can allow you to develop an eco-system with some early consumers who in turn can help drive the product in new and unexpected ways. That is, let the consumers tell you what they want. Not so revolutionary but worth remembering!

He also made the point, again worth remembering, that _how_ something works is less important than _what_ it can do, particularly in the context of innovation.

# [James Bligh (NAB) - Digital Innovation in a 150 year old bank](http://au.apidays.io/slides/bligh-nabapi-journey.pdf)

The second keynote on day 1 and who knew NAB was so, well ... cool?

He started off with a list of points on why they felt the need to innovate, which seems to sum up the problem for most modern, large sized companies: consolidation (to support cross selling), proliferation (mobile, tablet, web), and competition (in this case traditional banking, as well as _fintech_).

He stated that _tension drives creativity_, which is actually kinda interesting (but clearly depends on the source of the tension, I imagine!)

He also aid that, for NAB, an API is the most cost effective and flexible strategy for reaching and reacting to their customers. Cool.

They also discovered a lot of unknown (or unexpected) usage, and had to adapt quickly, not just to maintain their service but to take advantage of opportunities as they arise.

Their architecture is actually pretty neat. They still maintain their core banking system (from probably decades ago) and enterprise service bus, with 18 month (yikes!) releases, which all must conform to the various government regulations. But, sitting on top of that is a bunch of _service engines_ (read micro services) that give them far more agile capabilities for web and mobile apps. This provides them a way to integrate the different modes of change and different stakeholders at different levels.

Obviously, this was a massive undertaking and has been ongoing for some time (5+ years?). However, they approached it from a small-steps perspective (what, no more big-bang, $100mil projects? How surprising ...) and managed to define boundaries within the organisation to begin segregating services, which could then be built out one at a time into the various service engines. It would be interesting to find out how they manage to separate those pieces, which are often tightly and often surprisingly coupled. (He mentioned strict governance, which would help if there is a strong hand in what's in and what's out.)

One last thing James said, which I quite liked was (and I'm paraphrasing a little): 

>when faced with a choice, which one is more awesome? Which one are you/ would you be proud of?

Seems like a pretty good way to make a decision :)

# [Kirsten Hunter (Akamai) - Irresistible APIs](http://au.apidays.io/slides/hunter-irresistable-apis.pdf)

This was another intersting presentation, focused on what makes an API great? What makes it something consumers want to use?

Not surprisingly, her advice was to focus on the business value, not the tech. But she presented it from the perspective of telling a story and focusing on what does your API enable? Why is it useful?

She also touched on how to measure the success of an API? And it's not just not just API key count :) You should be asking how are your users using your API? How active are they? Are they returning? Are they using it the way you want/intended?

And most of all, are you capturing this data? (hint: you should be, even if you're not actively using / mining it right now, you may well be tomorrow).

Some guidance she offered included don't surprise your users and REST is not always best. Focus on usability and your driving use cases, not REST perfection. Also focus on _deliberate design_ - she stressed that governance was important in ensuring that an API stayed focused and coherent.

Coming back to governance, she echoed one of the themes of the conference, which was on designing your API schemas in some modelling language (raml, swagger, blueprint, dsl?). The schema then becomes an artefact for use with developers, stakeholders and the exec level. Stay focused on the why. 

Interestingly, Akamai has an API working group enforcing schema model before API release, which acts as a contract. Too heavyweight? Don't know, but seems like it could be beneficial in a larger organisation when there are competing forces. Of course, design by committee isn't usually my first choice :)

# [Michael Hyatt (MuleSoft) - User delight driven design of APIs](http://au.apidays.io/slides/hyatt-user-delight-driven-apis.pdf)
 
Live demo of RAML to create an API schema in AnyPoint (from MuleSoft). Mentioned APX (API experience design), is that a thing now?

One interesting thing about RAML is that it has the concept of traits (such as marking a collection as having an order).

# [Rob Zazueta (TIBCO Mashery) - The RESTed NARWHAL](http://au.apidays.io/slides/zazueta-rested-narwhl.pdf)

This presentation focused on the [NARWHL](http://www.narwhl.com) design framework for thinking about how to design adaptable API's.

NARWHL stands for **N**oun as **A** **R**esource **W**ith **H**yper**L**inks and is a resource oriented architecture (not service oriented arch).

From the website:  

>Where REST is an architectural style for APIs, NARWHL is a framework intended to provide a roadmap for those needing to implement an API using current best practices but flexible enough to grow into the future.

They have also defined their own [NARWHL Maturity Model](http://www.narwhl.com/narwhl-maturity-model/) similar to the [RMM](http://martinfowler.com/articles/richardsonMaturityModel.html).

Also briefly mentioned Hypermedia (as everyone did), describing it as something that you _describe_, not _define_.

Oh, and categorically stated that client SDKs suck ... but are completely necessary right now. Ouch.

# [Shelby Switzer (Healthify) - APIs, Spreadsheets and Drinking Fountains](http://au.apidays.io/slides/switzer-apis-drinking-fountains.pdf)

This one was kinda cool from a community perspective. She talked about how local communities are accessing government (and other) data and using it for the betterment of their local communities (be it avoiding parking fines to helping people find free parking spaces).

She also has an interesting GitHub project up called [API in a box](https://github.com/switzersc/api-in-a-box). From the README:

>API-in-a-Box is exactly what it sounds like. Say you have a handful of CSV files that you need a searchable API for. Put those files in Github repository, spin up this API-in-a-Box, and there you go! A REST hypermedia API that utilizes Elasticsearch's killer searching.

It was interesting to see the unexpected uses of open data. If data is not made available, then these connections will never be made, no matter how much _innovating_ government (or other) tries to do.

# [Graham Lea (Tyro) - Building a bank out of micro services](http://au.apidays.io/slides/lea-microservices-bank.pdf)

These guys where a payment gateway, but their customers where hurting due to the banks delays in moving money from one account to another. So they decided to become a bank! Nice. They also did it to take advantage of the flexibility and low time to delivery for MVP type features. Even nicer!!

He started off with a paraphrased take on Cockcrofts definition of a micro services architecture, describing it as a _loosely coupled distributed architecture with bounded contexts_.

I believe the original is:

> ... a service-oriented architecture composed of loosely coupled elements that have bounded contexts.

I like the addition of distributed in there, but he also had a whole list of guidance around building APIs. He recommended ensuring a _single responsibility for each service_, and that you must define and document your services. He talked about _responsible services_, which are services that use as few other services as possible.

He also touched on _data ownership_, and that it's a good idea to have one schema per service, independent of all other services. In this way you can avoid inappropriate joining (why does that sound so funny? ... ahem)

More tips included caching data where processing happens, preferring async communication wherever possible and that if two services are very chatty then they are probably the same service (hint: combine them into one, or reconsider their contexts, because their boundaries are not well defined or separated). They also used [Pact](https://github.com/realestate-com-au/pact) for testing.

One more general piece of advice he gave was to organise the team around the work. This is really good to remember, as organising the work around the team is just silo'ing and shifts focus away from features / business value. 

# [Steven Willmott (3scale) - Entering the platform age](http://www.slideshare.net/3scale/entering-the-platform-age-how-to-create-genuine-value-for-internal-and-external-api-consumers)

The keynote from day 2, and stressed again the need for governance and communication around your APIs. He also made an interesting point about the shift from 1-1 to 1-N client server interactions, and even further to N-N interactions with the proliferation of both connected devices and services.

He made a great point that the value of any platform lies in allowing co-creation between providers and consumers. Makes sense.

He also used put up a diagram with expectation on one axis (expected to unexpected) and outcome on the other (desirable to undesirable). He then made focused on the undesirable outcomes and made the wonderful connection of innovation as something that is _unexpected_ and _desirable_. He also described the alternative of _unexpected_ and _undesirable_ as a fire drill :)

Other interesting guidance was to not focus on the developer, as although they may be the _enabler_ of the user, it is actually the user who really consumes your API (hint: focus on the why? of your API, not the how?) Logically following on from this he noted that the measure of success of an API is not the number of hits, but the number of businesses (or amount of business value) enabled. 

One last bit of advice was that voice activation / commands will change APIs because they will need better ordering and filtering, it's simply not good enough to return just pages of data. Not sure I have an opinion, but it is interesting to think about how the if the consumers usage changes subtly (typing in a search box to asking Siri to find a nearby restaurant), it could have ramifications for your APIs usability.

# [Uli holtel (BankWest) - following the signs](http://au.apidays.io/slides/holtel-follow-the-signs.pdf)

This one was about hypermedia, which he uniquely described as runtime intellisense for REST APIs! 

He did have some other guidance, based around what level of coupling your API and client can successfully support. Some scenarios to keep in mind are: Internal versus external; API ownership; Single versus multi-client; Process ownership (are you the thought leader of the process?); Rate of change; and API context sensitivity (how sensitive is your API usage to web client, mobile device, tablet etc).

He also mentioned using [Postman](https://www.getpostman.com) as a tool for exploring API. I haven't used this before, but looks quite nice.

# Tim liddlelow (ANZ) -  an API primer (no slides link available)

This was kind of a surprise. He had some really thoughtful stuff to say on designing your APIs, and that APIs are about exposing your business data to a consumer not an app programming interface in the traditional software library sense.

The quote of the conference for me (paraphrasing a little):

>APIs are 20% tech and 80% people/ business.

He also noted that API management is very different to desktop applications or even web applications management, but it's crucial to monitor your API and track usage analytics.

# [Brett Adam - API or die trying](http://au.apidays.io/slides/adam-api-or-die-trying.pdf)

Some really useful insights into building APIs. Again he reinforced the need to gather analytics for your API. Things like usage, context and work flows. You should also keep in mind that you need to correlate usage with accounts as
people will use your API in ways you never imagined and you want to see that data.

He mentioned the [Charles](https://www.charlesproxy.com) tool for watching http traffic and noted that you really need to be aware of what can be sniffed from your API (obviously this will be more of less serious depending on the data you're sending).

Quote of the presentation:

>Use HTTP / REST and get over it :)

He talked a bit about rate limiting and that it can be a good idea to include a "retry after" meta data element in http header.

He also noted that side-loading is OK. Be pragmatic about it and pre-package data if necessary. You don't have to deliver everything over your API. And get your versioning sorted early!

He posed the question: Why is rest the only real API?

The answer being the enormous amount of machinery between the user and back end (proxy, firewall, servers) and that you're likely to be hitting a different server every request at scale. The point being these things only work well with REST, building on all the intelligence (caching etc) along the way.

# Adeel Ali (Apimatic) - Apis in the real world (no link to slides available)

These guys analysed around 11,500 APIs! Some of the findings where that 70% didn't include an authentication type in a discoverable way and that only 12% included category information. Honestly I'm not sure of the significance of either of those, but it does speak to the larger issue of discoverability of an API. If you're going to make a public API then make it discoverable! Or don't make it public. Geez.

He also stressed (probably because they've tried to build an automated API discovery tool) that you really shouldn't violate the basic tenants of HTTP (safety, cachability, idempotency), but otherwise do what best suits your need.

# [Nick ward (MS) & Jorge Arteiro (Kloud) Mobile innovation in the mobile first, cloud first world](http://au.apidays.io/slides/ward-arteiro-api-innovation.pdf)

Microsoft have consolidated their APIs! [Try it out here](http://graph.microsoft.com).

It's kinda awesome sauce (any parents of Furby toting toddlers out there?)

And MS has a complete API reference here [aka.ms/apiref](http://Aka.ms/apiref).

Oh, and then there's [Project Oxford](https://www.projectoxford.ai) - a bunch of AI based APIs for speech, vision and language. Awesom_er_ sauce ;)

# Rob Valk (Sixtree) - Scaling the bikeshed with Jason API

Provided some nice thoughts on how to think about your API and that's it's a
resource graph, not domain graph. Trotted out HATEOS again, which is the Worst Acronym Ever (WAE?).

He talked about _bikeshedding_, a term I hadn't heard before, but means spending too much time on trivial issues. It comes from [Parkinsons Law of Triviality](https://en.wikipedia.org/wiki/Law_of_triviality) - go read the Examples section (it's pretty funny), but it revolves around a local council debating the colour of a bike shed that was to be built next to nuclear reactor.

He also mentioned JSON API (which is derived from emberjs I believe?) and that it's best to use a library ([there are plenty available](http://jsonapi.org/implementations/). One interesting feature is that you can use the _include_ property to force linking to duplicated entities (and this is why you want to use a library to automate the construction of the JSON!)

JSON API also plays much nicer with dynamic languages, but less so with static languages where the effort to parse the structured JSON back into objects is onerous (hence (again) the use of libs).

# Summary

Overall quite an interesting and diverse bunch of presentations. I liked the repeated focus on designing your APIs well, in a cohesive and discoverable way.

API management also came up a bit, although no one really offered much in the way of a solution or guidance, other than it's difficult and requires attention.

Design first was also a major topic, but again there are lots of options available here. Just keep focused on _why_ you are building your API.

Lastly, there where a number of people who described a split in their development teams, almost always around the API "layer". I think this is OK, so long as people are not pigeon holed on either side and everyone is involved in the API design.










