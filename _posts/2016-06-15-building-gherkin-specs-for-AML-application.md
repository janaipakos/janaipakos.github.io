---
layout: post
title: Building Gherkin Specs for an AML Application
date: 2016-06-15
---


Much of this post was inspired by [*Specification by Example using Gherkin*](https://www.manning.com/books/specification-by-example-using-gherkin).

In enterprise organizations, specifications are confused with tasks. Rather than providing a large description of the system or application in the form of specifications, or a list of requirements that describe the capability of the software, test and design documents focus on performance goals for software testers (read: implementation). Oftentimes, this segmentation does not give a clear picture of how an application performs or even what its purpose it, and this methodology only helps testers. But this is also not helpful, as testers only focus on their responsible tasks. For anyone else reading the document, the specification is too granular, and, to use a cliché, misses the forest for the trees.

Alternatively, specification by example focuses on defining requirements or software capabilities by illustrating specifications. 

The difference in these two methodologies is a clearer overall goal and a more helpful specification document. 

Below is a sample anti-money laundering application. Monetary transactions are screened by location and amount, and if either of these values fall into a certain range, they will be flagged by the system and require a closer inspection.

Let’s screen three sample transactions:

```
{ID: 1, location: USA, amount: 5000},
{ID: 2, location: Mars, amount: 1000},
{ID: 3, location: USA, amount: 10000}
```

Our traditional or enterprise UAT document may look like the following:

```
-Step: 1, Tester: James, Task: Record transaction ID 1 to database, Expected Result: Confirm transaction not flagged
-Step: 2, Tester: April, Task: Record transaction ID 2 to database, Expected Result: Confirm transaction flagged
-Step: 3, Tester: Bob, Task: Record transaction ID 3 to database, Expected Result: Confirm transaction flagged
```

This “documentation” has problems. From a tester perspective, I have no idea how this system works, or even its possible results. The only thing that interests me, in this case tester James, is making sure the ID 1 transaction is not flagged. I have no idea why or how flagging occurs, and I don’t care about the other transactions. In a classic case of CYA, I'm only focused on what test case my name is attached to.

From the perspective of any non-tester, this document tells us nothing about the application or software. Deductive reasoning tells us that this system flags transactions for any number of reasons: locations other than USA, Mars as the location, locations not a string of three characters, locations in lowercase. Similarly, the amounts may need to be 5000, start with the digit 5, or be four digits in length. There are a litany of unknowns. And it leads to a case of shortsightedness and mystery.

Compare this to a specification: 

```gherkin
Feature: Screen valid transactions
Scenario Outline: Valid transactions should not be flagged

Given a transaction
 | ID   | location   | value |
 | <ID> | <location> | <value> |
When <ID> is passed through the AML application
Then it <should?> be allowed to go through

Example: Allow only transactions with correct fields
   |ID | location  | value  | should?   |
   | 1 | USA | 5000 | should    |
   | 2 |     | 5000 | shouldn’t |

Example: Allow transactions with locations in USA
   |ID | location  | value  | should?   |
   | 1 | USA  | 5000 | should    |
   | 2 | Mars | 5000 | shouldn’t |

Example: Allow transactions with values under 10000
   |ID | location  | value  | should?   |
   | 1 | USA | 9999 | should    |
   | 2 | USA  | 10000 | shouldn’t |
```

The explicit criteria helps anyone reading the specification verify its requirements. There is much more to this, including creating one source of truth in a living document represented by a specification suite, and the testable code usable with Cucumber. But the focus of this post is to show the difference in tasks and specifications, and to show that a more descriptive approach is not a detriment to a test document.
