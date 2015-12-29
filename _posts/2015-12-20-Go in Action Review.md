---
layout: post
title: Go in Action Review
date: 2015-12-20
---

*Go in Action* begins with a quick-start look at a Go program that implements typical functionality found in a Go program. Following this introduction, the remaining eight chapters examine important concepts included in this starting program, including the basic unit of code organization in Go, called packages, and the independent execution of coroutines, called concurrency. These are two areas handled effortlessly in Go.

While the reader does not necessarily build a Go program from scratch, *Go in Action* includes a large number of examples with each introduced concept, and encourages the reader to try the code examples in the online Go Playground. The examples cover a variety of problems, such as introducing user types and unit testing, that demonstrates correct and troubleshot code, resulting in a more thorough look at the language and common chokepoints.

One of the most exciting concepts in web development is reusable packages, which is something Go handles very elegantly. Chapter 3 gives an overview of Go packages and build tools, with a clear description of the best practices when creating packages, and the options available in project structuring, vending, and dependency management. Chapter 8 provides examples of a few of the more popular standard library packages, such as a logger and a JSON parser. The examples here are easy to understand and implement in your own projects, and they show the kind of practically that is frequently presented in Go. Similar to Meteor.js, much of Go has features “out of the box” that would be a hassle to implement in other languages or frameworks, such as concurrency in Node.js.

The book’s visuals enhance concept explanations. Slices, pointers, maps, and concurrency are all topics that are more clearly explained through the accompanying graphics. Especially helpful, albeit very strange, are the illustrations in Chapter 6 showing synchronization between goroutines using buffered and unbuffered channels. The images here are rarely hand-drawn, which is one of my gripes with other Manning titles.

Testing is easy in Go. Unit testing and benchmarking can happen alongside developments with the ‘go build’ and ‘go test’ commands. Furthermore, the book excels at not only introducing how Go handles these concepts and practices, but also provides definitions and examples that ensure beginners can quickly get up to speed on these important topics, even though the title is presented for experienced developers,

Overall, *Go in Action* is a great introduction to not only the language but also modern web development.

Disclosure: (Manning)[https://www.manning.com/books/go-in-action] provided my copy of *Go in Action*.
