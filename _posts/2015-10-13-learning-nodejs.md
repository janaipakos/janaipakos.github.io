---
layout: post
title: Learning Node.js
date: 2015-10-13
---

It's been about 100 days since I've started learning Node.js.


While print books are rich with information and helpful in explaining concepts, the projects and referenced modules are sometimes outdated.

The best resource I found was NodeSchool.io(www.nodeschool.io). NodeSchool features explanations and exercises delivered and followed through the command line. Because it is on GitHub, the questions are always up to date, and there was never an instance where I tried to perform an outdated command.


Other methods I tried was online projects. While the finished product was working as intended and often pretty neat, the short-attention span of web users caused the instructors to rely on education by replication. Much of the time I would copy and paste large chunks of code with only a small explanation by the writer. The result was a new application, but confusion on how I actually got there.


Print books were more in-depth. NodeJS in Action from Manning explained concepts fully before moving on to the next. The problem with this medium was one of speed: the title spent several chapters on the Connect middleware, something made obsolete by the framework Express, which leverages Connect with added sugar. Additionally, the voting app project featured huge inconsistencies across chapters. This is indicative of the problem with technical books, but the multiple authors' were representative of the striated documentation of the Node.js stack at large.


This is not even mentioning the finicky nature of Node.js in relation to its callbacks and, in my opinion, cumbersome nature in regards to authorization. For example, using Passport, an authentication module, to connect users with a Google consent screen takes around 20 lines. A framework such as Meteor.js does it in one.
