---
layout: post
title: Corporate JavaScript Style Guide
date: 2015-10-29
---
### Corporate JavaScript Style Guide

The following is a JavaScript style guide combined from various corporate and enterprise jobs. The corporate guide's I've read wed the cold, hard practicality of big business with modern practices such as code testing. The three important characteristics of good code is readability, security, and consistency, and it's no surprise that big old school businesses like to structure their code in an orderly, risk-averse manner.


####JavaScript (not related to Java) is a front-end language that does not interact with the database or interfaces###
####Limit line length to 120 characters
 - This is 50% longer than the suggested line length of 80 encouraged by other style guides. I attribute this to companies not using GitHub (version control is, however, encouraged).
####Use double-quotes over single-quotes
 - This helps Java developers read the otherwise indecipherable JavaScript code.
####Use /* for comments, and favor block comments over single-line
 - "Cover your ass" is a phrase I hear often, and over-commenting code is a failsafe against accountability when something breaks.
####Spaces over tabs, with 4-space indentation for readability
 - While file's are huge and unwieldy, I appreciate the attempt at clarity.
####Use JShint to test for errors in code, and delete commented out code and outdated comments
 - Two bombshells that go against the status quo of waterfall development and bloated projects.

