---
layout: post
title: MongoDB Model Tree and Replication Comparison
date: 2016-05-06
---

While studying for the MongoDB Developer Exam, I noticed that many structures and sets, while described thoroughly in the documentation, lacked an easy to read visual component. Below are two tables I came up with for drills.

## Model Tree Structures


| Structure   | Read  | Query   | Write     | Subtree     |
|-----------  |:----: |:-----:  |:------------- : | :---------------------- : | 
| Parent      |   Good  |   Poor   |       Poor      |         Poor          |
| Child       |   Good  |     Poor   |      Poor      |         Poor          |
| Ancestor    |   Poor  |   Good   |      Poor      |         Good          |