---
layout: post
title: Isomorphic JavaScript Applications
data: 2016-10-04
---
Isopmorphic JavaScript applications share JavaScript code between client and server. There are several perks to this, including a codebase with an equal form regardless of environment.

Below are a few key points from [*Building Isomorphic JavaScript Apps*](http://shop.oreilly.com/product/0636920042846.do) by Jason Strimpel. Strimpel uses an eCommerce site as a barometer for three qualities a modern web application should fulfill: 
1) Should be indexable by search engines to improve SEO
2) Initial load should be fast
3) Future page should be fast

Specifically, the eCommerce page must show up first in searches in order to get customers, and then load fast in order to keep them. Modern applications should have SEO support, distributed rendering, a single code base, an optimized page load, and a single stack.

## Web Application History
A classic webpage is made up of HTML, the Uniform Resource Identifier (URI) that shows the name of the server that will respond, and the Hypertext Transfer Protocol (HTTP) that connects everything. Everything is rendered on the server, then JavaScript renders this content to the browser. Of our three criteria, this fulfills the first two (indexable and fast initial load) but this method still needs to reload the entire page when routing.

Then came AJAX, which focuses on fetching relevant information in the view layer. But this led to duplication and bugs via the two UI code bases.

Next up was Single Page Applications (SPA) which are entirely rendered on the client. This seperates logic from data retrieval, consolidates UI to a single language, and has a low impact on servers. SPA's are good and bad. They are good for future page loads (point three) but the initial load is sluggish because of the huge JavaScript file sent to the client. Additionally, there is no SEO because SPAs use hash fragments for routing (e.g. #about). Because these do not make a network request, SEO can’t be used and the sites can't be crawled. The solution is to use a headless browser in PhantomJS.

Now we have Isomorphic apps. These are a union between classic and SPA. They are good for SEO with History API, distribute rendering with a low server load, have a single code base to reduce the UI cost and bug count, optimize the initial page load, and feature a single JS stack. However, the author warns the reader that isomorphism is not necessary if an application doesn’t  need SEO, i.e. if it is behind a login screen.

## Types of Isomorphic Applications
There are two kinds of Isomorphic Applications- environment agnostic and shimmed.
- Environment agnostic can be used in Node or a bundler and used in any environment
- Shimmed is an abstracted or filled in mapping for every environment. In this case, abstractions such as if-then and var are needed

## Real Time Applications
Real time applications such as Uber or Slack push data from the server to the client while updating every client device with new data. These applicatons need a way to watch the database, a push tech such as Websockets or long polling emulation, and a cache to avoid repeat trips. On the other hand, Isomorphic API has bidirectional data sync, and client simulation on the server. And this is not simply running SPA on the server.
- There are the same API commands for the client and server, leading to a dry codebase with the same tests and same updates
- Similar to Meteor, the server, DB and client cache are kept in sync
- The server proactively sends data client. The server effectively simulates the client, updates the server, then sends these changes to the client

## Abstractions
The book also discusses leaky abstractions. Generally, abstractions should not solve nonexistent problems, such as creating an API wrapper around a library in case it later needs to be swapped out. This may never happen! Abstractions should have an immediate value. Think longevity rather than premature decisions. A few common abstractions include getting and setting c ookies or redirecting requests. These encapsulate environmental specific details.

## Modern Application Functionality
There is also a list of important functionalities or steps for modern web applications:
- Routing- routers should map the URL to a function
- Exeuction- should be asynchronous
- Response/Render- should be async after execution
- Serializing- any data retrieved in the previos steps should be part of the response
- Deserializing- objects and data need to be recreated on the client
- Attaching- event handlers should be bound for interactive applications

## Closing Thoghts
Generally I thought this book did a good job of introducing Isomorphic applications to the reader, and how this concept fixes several problems facing (and have been facing) web development for a while. The author is clear in his arguments and keeps returning to them after looking at possible solutions. The last part of the book also has a few case studies of larger organizations using Isomorphism on their projects, including Node/React and Angular 1/Angular 2. While the high level explanation is great, I would have preferred more code examples to follow along with. 
