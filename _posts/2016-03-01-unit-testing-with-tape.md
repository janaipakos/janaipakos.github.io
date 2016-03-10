---
layout: post
title: Unit Testing with Tape
date: 2016-03-01
---

Tape is a TAP (Test Anything Protocol) producing test harness for Node.js and browsers. It interacts with testling, which runs unit tests in all the browsers and outputs TAP. Unit tests are small, automated tests that test a small piece of functionality. The suites of automated tests grow alongside the application, and warns developers of failing code or broken code as the results of introduced changes. Unit testing makes developers more confident in code refactoring, ensures the application can be changed easily as its grows more complex, and ensure code quality.


## Test-driven development ##

Test-driven development encourages developers to create unit tests first and then write the supporting code. This code is designed to be only minimum passing code. TDD is supposed to encourage developers to create unit tests throughout the development process. I don’t use TDD because I find it less intuitive and containing more overhead that writing tests for code that is already written. While code of course will change in future iterations, initial code will almost definitely change.


## tape ##

Tape is a lightweight unit testing application available through npm. I prefer tape for three reasons it is lightweight and simple too implement. It's very flexible; you can run it in the browser console or through the command line. And it is easy to write, and it does not create global objects as other testing frameworks do. I used tape for a very simple application that multiples any input that is a whole number by 666.


After designing the application, I determined six different criteria to follow. The unit tests for these are straightforward with tape.


The user creates the number of steps for each test, and then compares the expected result against the actual results. Tape runs these tests and displays them in the console of a test runner html page. Each unit test has a particular criteria that it writes at the head of each test to make it easy to read and match the results for each test. Running these tests with each new change takes a second to do and it’s much more thorough and transparent than simply running a SQL script once or screenshotting Microsoft SQL server management and declaring the application tested. Yes, I have seen this.


This also helps from a documentation and audit perspective: the objective of each test is explicitly written with each unit test function.


Overall, testing should be easy, and tape is lightweight, unobtrusive, and easy to write.  The following is a definition of the application and the derived test cases.


## Application Definition ##

In this application you input a whole number and then click on a button to multiply that number by 666. The resulting number is displayed in a list. Any error, such as an invalid or decimal number, is also displayed in the list. There is also a button to clear the list. There are six derived test cases based on this functionality


## Derived Test Cases ##

- Clicking Satanize without an input should result in an error message.
- Clicking Satanize with a decimal input should result in an error message.
- Clicking Satanize with a whole number input should result in a number multiplied by 666.
- The resulting number should be displayed in a list, along with any error message.
- Clicking clear with no input should not throw an error.
- Clicking clear should clear the results list.
