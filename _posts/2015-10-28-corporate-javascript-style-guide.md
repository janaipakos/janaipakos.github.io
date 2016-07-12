---
layout: post
title: Corporate JavaScript Style Guide
date: 2015-10-29
---

The following is a JavaScript style guide combined from various corporate and enterprise jobs. The corporate guides I have read combine the cold, hard practicality of big business with modern practices such as code testing. The three important characteristics of corporate code is readability, security, and consistency, and it's no surprise that big old-school businesses like to structure their code in an orderly, risk-averse manner.


## JavaScript is a front-end language ##
- Enterprise style guides refer to JavaScript as a client-side programming language. Some even have reminders that Java and JavaScript are not the same langauge. These guides do not take into account Node’s server-side interaction with databases and interfaces.

## Limit line length to 120 characters ##

- 120 characters is 50% longer than the suggested line length of 80 encouraged by other style guides. I attribute this to companies not using GitHub, or any type of version control..

## Use double-quotes over single-quotes ##

- “Cover your ass” is a phrase I hear often, and over-commenting code is a failsafe against accountability when something breaks. By encouraging double-quotes, corporate style guides nudge developers to think of their code base as a “narrative” to air grievances and craft confusing and jargon filled asides.

## Favor block comments over single-line ##

- The trend of writing complex code that is covered in comments may be the lesser of two evils (no comments at all). However, eliminating the need for comments through clear function and class names is not mentioned.

## Spaces over tabs, with 4-space indentation for readability ##

- While files are huge and unwieldy, I appreciate the attempt at clarity.

## Use JSHint to test for errors in code, and delete commented out code and outdated comments ##

- Just kidding.

