---
layout: post
title: Learning Node.js and Enterprise JavaScript
date: 2015-10-13
---

I started learning Node.js 100 days ago, the same day I started consulting an IT department. Learning about sanction screening and anti-money laundering during the day and Node's idiosyncractic behavior at night has been fun. I'm not entirely in love with it, and I'll see if my attitude changes at day 200, but it has helped me think about programming in a different way.


It's also made me think about enterprise languages. The past few months I have been surrounded by Java and .NET developers, and their lumbering, monolithic stacks. Starting a server in Node.js is done with a command line `serve`. Here, I need to submit a ticket, and wait a week for the new environment to be recreated. Nevertheless, I think that microservices and modular programs, rather than large deployments on the Java and .NET stack, are going to change enterprise architecture and programming models.


I've been reading a lot of books about Node.js, and the following is a mix between review, primer, and predictions.


Some background. Node.js uses non-blocking I/O, meaning it can keep up with mobile traffic volume. There are many metaphors for this--*Node.js in Action* by Manning Publications[^1] uses the ordering and preparation of hamburgers in a fast-food restaurant as an example. A report from Forrester Research uses Santa taking trips back and forth to the North Pole. Both illustrate the problem with persistent server connections--long wait time for users. Servers with non-blocking I/O can use a single thread while performing the least amount of work for all requests. This asynchronous, event-driven architecture can be found in Node.js.


JavaScript is not going to replace Java and .NET in enterprise architecture. Instead, it will find a supplementary role similar to the cherry-picking of Agile and XP by managers. Node.js does a great job of aiding software development and connecting existing services for modern companies, but a full replacement is likely to be met with resistance. The reason for this is Node's double-edged nature.


It is fast. Modular developers can fix small changes in a JavaScript stack, without needing to understand back-end Java or .NET. Rather than taking days to create an environment in Java or .NET, developers can deploy environments in Node.js in seconds, and new features and frameworks can be plugged-in with one command line through the node package manager.


This is great for small to medium projects and small teams. Rapid change is helpful in prototyping, but what happens when this awesome architecture is deprecated and documentation is outdated? Or the Node.js team splits into Io.js, MEAN.js, or MEAN.io (for example)?


This was my biggest gripe with the material in technical print books. While they were rich with information and helpful in explaining concepts, the projects and referenced modules were sometimes outdated. *Node.js in Action* explained concepts fully before moving on to the next. The problem with this medium was one of speed: the title spent several chapters on the Connect middleware, something made obsolete by the framework Express, which leverages Connect with added sugar. Additionally, the voting app project featured huge inconsistencies across chapters.


This is problem with not only technical books, but also the scattered documentation of the Node.js stack in general, and even moreso with the MEAN stack.


The best resource I found was NodeSchool.io(www.nodeschool.io). NodeSchool features explanations and exercises delivered and followed through the command line. Because it is on GitHub, the questions are always up to date, and there was never an instance where I tried to perform an outdated command.


But back to Node.js in general. Additionally, when features are easier to implements, and developers are working in their own kind of candy shop, scope-bloat and unecessary modules find their way into the application.


Less important is the language than the concepts of event-driven and functional. Event-driven means updates and features can be chained to different applications. For example, instead of recreating appliation environments to make changes, an event handler can asynchronously fire once the business logic changes. Think of this as future-proofing in the face of compliance changes, similar to connecting a future condition change to the Bitcoin blockchain.


There is still a lot I don't `get` with Node.js. Callbacks are a drag, and authorization is cumbersome, even with Express. For example, using Passport, an authentication module, to connect users with a Google consent screen takes around 20 lines. A framework such as Meteor.js does it in one.


This goes back to what I love about Node.js. Some of it is magic and the answer to so many headaches in enterprise systems. Some of it is voodoo that I can't wrap my head around. Anyway, I'm sure some of this will clear up during the next 100 days.


[^1]: [*NodeJS in Action*](https://www.manning.com/books/node-js-in-action)
[^2]: [Forrester](https://forrester.com/home)
