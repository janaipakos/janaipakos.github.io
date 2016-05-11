---
layout: post
title: MongoDB Model Tree and Replication Comparison
date: 2016-05-06
---

While studying for the MongoDB Developer Exam, I noticed that many structures and sets, described thoroughly in the documentation, lacked an easy to read visual component. Below are two tables I came up with for drills.

## Model Tree Structures
As Model Tree Structures get more verbose, they become both easier to query against and require fewer queries. However, these more advanced Model Tree Structures are also more difficult to write, and are recommended for static structures rather than subtree modification. 

For example, adding one node to a Nested Model Tree will require the modification of two fields (left and right) *for each entity*. As a refresher, the Nested Tree Model looks like this: `db.categories.insert( { _id: "Books", parent: 0, left: 1, right: 12 } )`. 

This is a huge waste. For another example, the Ancestors pattern, which looks like this:

`db.categories.insert( { _id: "dbm", ancestors: [ "Books", "Programming", "Databases" ], parent: "Databases" } )`) 

is similar to the Materialized Paths pattern:

`db.categories.insert( { _id: "Databases", path: ",Books,Programming," } )`

but is actually slower while being easier to use.  Speed and flexibility are the trade-off. There are four main performance options for these Tree Structures: speed during reads, the number of needed queries, speed of writes, and the updating of subtrees.

| Structure   | Read  | Query   | Write     | Subtree     |
|-----------  |:----: |:-----:  |:------------- : | :---------------------- : | 
| Parent      |   Good  |   Poor   |       Good     |         Good          |
| Child       |   Good  |    Good   |      Good      |         Poor          |
| Ancestor    |   Good  |   Good   |      Poor      |         Good          |
| Materialized    |   Good  |   Good   |      Poor      |         Good          |
| Nested    |   Good  |   Good   |      Poor      |         Good          |



## Replica Set Members
Once the user's model is created, they can start figuring out if replication is needed, as well as how they want to separate their servers across data centers.  Below is a chart of the different types of servers available in a replica set, and their available attributes. There are four options: if the replica set can be queried, vote during elections, copy data from the oplog, and be elected as a Primary.

| Server   | Query  | Voting   | Data     | Electable     |
|-----------  |:----: |:-----:  |:------------- : | :---------------------- : | 
| Primary     |   Yes  |   No   |       Yes      |         No         |
| Secondary     |   Yes  |     Yes  |      Yes     |         Yes         |
| Arbiter    |   No  |   Yes   |      No     |         No          |
| Hidden   |   No  |   Yes   |      Yes      |         No         |
| Non-voting    |   Yes  |   No   |      Yes     |         Yes          |
| Priority 0    |   Yes  |   Yes   |      Yes      |         No         |


<br /> 
For more information about MongoDB, its positives and negatives, and its Developer and DBA exams, visit the main site [here](https://www.mongodb.com).