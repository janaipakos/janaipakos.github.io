---
layout: post
title: Learning Node.js and Enterprise JavaScript
date: 2015-10-13
---

I started learning Node.js 100 days ago. This is the same day I started consulting for the IT department in an international company. Learning about sanction screening and anti-money laundering during the day and Node's idiosyncractic behavior at night has been fun. I'm not entirely in love with it, and I'll see if my attitude changes at day 200, but Node.js has helped me think about programming in a different way.


First off, Node has helped me analyze enterprise languages. For the past few months, I've been surrounded by Java and .NET developers, and their lumbering, monolithic stacks. Starting a server in Node.js is done with one command line. Now, I needed to submit a ticket, and wait a week for the new environment to be recreated. Nevertheless, I think that microservices and modular programs, rather than large deployments on the Java and .NET stack, are going to change enterprise architecture and programming models.


## Learning Node.js
I read a few books while learning Node.js. The following is a mix between review, primer, and predictions.


Node.js uses non-blocking I/O, meaning it can keep up with mobile traffic volume. I came across many clever metaphors illustrating this concept--[*Node.js in Action*](https://www.manning.com/books/node-js-in-action "Node.js in Action") (Mike Cantelon, Marc Harter, T.J. Holowaychuk, Nathan Rajlich, 2013) uses the ordering and preparation of hamburgers in a fast-food restaurant as an example. A report from [Forrester Research](https://forrester.com/home "Forrester Research") portrays Santa taking trips back and forth to the North Pole. Both illustrate the problem with persistent server connections--a long wait time for users. Servers with non-blocking I/O can use a single thread while performing the least amount of work for all requests. This asynchronous, event-driven architecture is where Node.js shines.


Experts predict that JavaScript is not going to replace Java and .NET in enterprise architecture. Instead, it will find a supplementary role similar to the cherry-picking of Agile and XP by company managers. Node.js does a great job of aiding software development and connecting existing services for modern companies, but a full replacement is likely to be met with resistance. The reason for this is Node's double-edged nature.


## Pros and Cons of Node.js
Node.js is fast. Modular developers can fix small changes in a JavaScript stack, without needing to understand back-end Java or .NET. Rather than taking days to create an environment in Java or .NET, developers can deploy environments in Node.js in seconds, and new features and frameworks can be plugged-in with one command line through the node package manager (npm).


This is great for small to medium projects and small teams, and rapid change is helpful in prototyping, but what happens when this awesome architecture is deprecated and documentation is outdated? Or the Node.js team splits into Io.js, MEAN.js, or MEAN.io (for example)?


This was my biggest gripe with the material in technical print books. While these books were rich with information and helpful in explaining concepts, the created projects and referenced modules were sometimes outdated. *Node.js in Action* explains a concept fully before moving on to the next. The problem with this title and the print medium is one of speed: the title spent several chapters on the Connect middleware, something made obsolete by the framework Express.js, which leverages Connect with added sugar. Additionally, the voting app project crafted throughout the book featured huge inconsistencies across chapters.


This is a problem found not only in technical books, but also the scattered documentation of the Node.js stack in general, and even moreso with the MEAN stack.


The best resource I found for learning Node.js was [NodeSchool.io](www.nodeschool.io). NodeSchool features explanations and exercises delivered and followed through the command line. Because they are on GitHub, the questions are always up to date, and there was never an instance where I tried to perform an outdated command.


## Event-driven Programming
But back to Node.js in general. Additionally, when features are easier to implements, and developers are working in their own kind of candy shop, scope-bloat and unecessary modules find their way into the application.


Less important is the language than the concepts of event-driven and functional. Event-driven means updates and features can be chained to different applications. For example, instead of recreating application environments to make changes, an event handler can asynchronously fire once the business logic changes. Think of this as future-proofing in the face of compliance changes, similar to connecting a future condition change to the Bitcoin blockchain.


There is still a lot I don't *get* with Node.js. Callbacks are a drag, and authorization is cumbersome, even with Express.js. For example, using Passport, an authentication module, to connect users with a Google consent screen takes around 20 lines. A framework such as Meteor.js does it in one.


This goes back to what I love about Node.js. Some of it is magic and the answer to so many headaches in enterprise systems. Some of it is voodoo that I can't wrap my head around. Anyway, I'm sure some of this will clear up during the next 100 days.
