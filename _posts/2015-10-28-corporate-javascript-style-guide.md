---
layout: post
title: Corporate JavaScript Style Guide
date: 2015-10-29
---

The following is a JavaScript style guide combined from various corporate and enterprise jobs. The corporate guides I have read combine the cold, hard practicality of big business with modern practices such as code testing. The three important characteristics of corporate code is readability, security, and consistency, and it's no surprise that big old-school businesses like to structure their code in an orderly, risk-averse manner.


## JavaScript is a front-end language ##
- Many enterprise style guides refer to JavaScript as a client-side programming language. Some even have addendums that JavaScript is not similar to Java. These guides do not take into accound Node's server-side interaction with databases and interfaces.

## Limit line length to 120 characters ##

- 120 characters is 50% longer than the suggested line length of 80 encouraged by other style guides. I attribute this to companies not using GitHub(version control is, however, encouraged).

## Use double-quotes over single-quotes ##

- I like this specification. This may be due to Java developers complaining about the otherwise indecipherable JavaScript code.

## Use /* for comments, and favor block comments over single-line ##

- "Cover your ass" is a phrase I hear often, and over-commenting code is a failsafe against accountability when something breaks. The trend of writing complex code that is covered in comments may be the lesser of two evils (no comments at all), but what about a rule such as eliminating the need for comments through clear function and class names.

## Spaces over tabs, with 4-space indentation for readability ##

- While files are huge and unwieldy, I appreciate the attempt at clarity.

## Use JShint to test for errors in code, and delete commented out code and outdated comments ##

- This is the most surprsing guideline I have come across. These are two bombshells that go against the status quo of waterfall development and bloated projects.

