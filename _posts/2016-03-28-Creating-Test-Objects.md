---
layout: post
title: Creating Functional Test Objects
date: 2016-03-28
---
Clear test logs not only help describe an application, but also help when debugging. As described in [*Specification by Example*](https://www.manning.com/books/specification-by-example) (Gojko Adzic, 2011), test logs can also serve as deliverables if no other documentation is available, as long as the logs have a few components: a brief description, an objective, a description of the test steps, test data (if required), the expected results, and the actual results. Descriptions do not have to be too lengthy. They can refer to functional requirements or the applications process.

The overall objective of the test log is to list the test objects that help describe the steps towards the functional result. But what should these test objects look like? Ideally, they are as small as possible, and only perform one thing. The functional requirements of a project can be broken into steps, which are then broken into subprocesses. This methodology is repeated until the creator reaches the foundational level, in which the test object only performs one function.

Web development follows this idea as well. Modules are installable packages through npm that do only one thing. React, Angular 2, and functional JavaScript separates components in order to avoid leaking and improve testability and shareability.

This test log made up of focused test objects can help describe functional specifications and change requests for management and executives. It can also be used during conversations between testers, developers, and architects during the entire creation process.

These test cases can be logged in a separate sheet and either attached to a larger testing document or passed to other testers to assist with User Acceptance Testing or Integration Testing. But keeping the test log (the implementation) separate from the functional requirements is important. Similar to the separation of concerns for components, the requirements or implementation should not influence the test data. Test case design should always be flexible to change based on the data, and not the other way around. These cases should be able to be revisited and reconstructed with new data.
