---
layout: post
title: Exorcising Ghost, Zombie, and Dead Code for Halloween
date: 2015-10-22
---
## The Mikado Method
The material for this post was adapted from [*The Mikado Method*](https://www.manning.com/books/the-mikado-method) from Manning Publications and authors Ola Ellnestam and Daniel Brolund. The Mikado Method is a process for iteratively working through legacy code by setting a goal, quickly trying a solutions, observing the solutions, **reverting** the changes, and repeating the process with a new solution. The key here is deleting code changes, which may or may not have worked, before trying something else, and avoiding a mud ball of change built atop change.


While the entire book is great, its appendix proves especially useful by including strategies to remove unused code. So for Halloween, here's how to remove ghost, zombie, and dead code.


## Types of Unused Code
Ghost code is code that may be commented out, and stay that way across releases. This may be a kind of Indian Burial ground situation, where the code was already there before it was placed under your charge. (In horror-speak, you moved into the house on the hill, hotel, cabin). Nobody knows what this code does, but you keep it around because it may be useful in the future.


Don't prevent a smooth transition into the afterlife--get rid of this code. It is never useful, and if it is, you can copy the code from a parent commit.


Zombie code refers to code that is neither dead nor alive. This is code that may not do anything, but is nonetheless included in automated tests, sucking the brains from maintenance resources. Ola and Daniel suggest cutting this code off at the head by removing the unit test altogether.


Without a test or call (or removed of life, in this example) zombie code turns into dead code. Dead code is like a derelict spaceship floating in space. Nothing calls it, nothing uses it, nothing tests it. Get rid of the baggage and delete it.


There are many tools that find uncovered code in production. Uncss, for example, will identify unused css. Hint: it is 90% of Bootstrap.


Steel yourself mentally before starting this process. Like ghost hunting, it is sometimes lonely, but ultimately satisfying to remove the weight of unused code.
