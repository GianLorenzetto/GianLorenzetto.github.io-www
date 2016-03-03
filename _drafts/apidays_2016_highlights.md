---
layout: post
title: APIDays 2016 Highlights
categories: [conference]
tags: [apidays]

---

# APIDays 2016 Highlights

# Steve Sammartino - Welcome to Startup Land

Keynote (1) Day 1
Horizontal thinking
Selling unfinished products
Creating eco systems
Connection of devices we never would have considered
How things work is less important than what it can do
Disruption

# James Bligh (NAB) - Digital Innovation in a 150 year old bank

Keynote (2) Day 1
Why? consolidation (cross sell, website), proliferation (mobile), competition .(trad, fintech), velocity
Tension drives creativity
API is most cost effective and flexible strategy for reaching and reacting to customer
Unknown usage, must adapt quickly
Service engines (micro services)
Still layered on top of enterprise bus, 18 mth releases, govt regs etc
Different modes of change and different stakeholders at different levels
Sprintboot docker/cloudfactory
API provides a solid security boundary
Faced with choice, which is more awesome? Which one are you/ would you be proud of?
Defined boundaries within organisation to segregate services, would be interesting to find out how they manage to separate those prices, which are often tightly and often surprisingly coupled. (Mentioned strict governance, which would help if there is a strong hand in what's in and what's out)

API experience / engagement

# Kirsten Hunter (Akamai) - Irresistible Apis

Tell a story, what does it enable. Why is it useful? Business value. 
How to measure success? Not just API key count. How are your users using your API? How active? Are they returning? Are they using it the way you want/intended?
Web vs API? API is cheaper ..
Guidance
Don't surprise your users 
Rest is not always best. Focus on usability and your driving use cases, not rest perfection
Deliberate design (harking back to governance)
If you don't focus on usability, you don't have to worry about scalability
Schema modelling (raml swagger blueprint) [dsl?]
Schema is an artefact for use with devs stakeholders exec focus on the why 
[github repo]
Akamai has API working group enforcing schema model before API release, acts as contract

# Michael Hyatt (MuleSoft) - User delight driven design of APIs 
 
Any point platform demo / raml
APX (API experience design) not sure that's a thing??
Raml has the comcept of traits (order able collection etc)
Mocks (ssoapui, raml-server, anypoint)

# Rob Zazueta (TIBCO Mashery) - The RESTed NARWHAL

A design framework for thinking about how to design adaptable Apis 
Narwhal.com
Noun as a resource with hyperlinks
Resource oriented architecture (not service oriented arch)
Resource relationships representations 
Different representations of the same resource based on different contexts
Trad way is to /prod/Id/web /mob etc
Use profile 
Include version here, not in uri
Same as web browser with plugins, search for handlers (not there yet)
Use specific mime types (ie, include the profile)
In band, part of uri
Don't define it, describe it (hypermedia)
Sdks suck but are necessary

# Michael Wise (Next Data) - Data science

Content over services. Everything delivered in the same way
Single source of truth, a unified view 
iPass (integration PasS)
Continuous data integration 
Data science behaviours-
Niche viscosity friction automation immediacy learning
Containers fo everything? Docker is good? Wha?

# Shelby Switzer (Healthify) - APIs, Spreadsheets and Drinking Fountains

API in a box GitHub switzersc
Social data mining

# Graham Lea (Tyro) - Building a bank out of micro services

Loosely coupled distributed architecture with bounded contexts (Cockcroft)
Single responsibility services (define and document)
Responsible services (use as few other services as possible)
Data ownership (own schema per service)
Prevents inappropriate joining
Cache data where processing happens 
Prefer async Comms
Chatty services indicates they're the same service
Pact for testing
Organise the team around the work
Micro services security questions
Built there own to take advantage of flexibility and low time to delivery for mvp type features
https://github.com/realestate-com-au/pact/blob/master/README.md

Micro services is a set of tools to solve problems in a distributed environment 

# Saul Caganoff (Sixtree) - Business process orchestration and Apis 

Foxycart (hypermedia)
Run my process
Hateoas
Event sourcing 

# Mike Amundsen - API: The "I" Stands for Innovation

Locknote Day 1
Ci and cd are about learning and learning fast











