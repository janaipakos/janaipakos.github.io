---
layout: post
title: Reporting Metrics for Project Management
date: 2016-02-12
---

While creating the testing and design documentation for a software application, my team transitioned through different project management methodologies until we found a reporting metric that was useful for both clarifying outcomes to stakeholders and for steering the project for the immediate team. We settled on two measurements, burn-down charts and throughput metrics, that tracked “features” in the form of documents. 

Due to the risk-averse client, our project had a set scope of one year, a linear or waterfall approach with set stages, a traditional process model with some opportunity for the team to decide on sprint length, and a discrete project delivery with a set go-live date and no continuous delivery.

The team decided on presenting metrics that were informational and diagnostic, in the case that we needed to call attention to a problem. 

 [*Agile Metrics in Action*](https://www.manning.com/books/agile-metrics-in-action) (Christopher W. H. Davis, 2015) and [*Software Development Metrics*](https://www.manning.com/books/software-development-metrics) (David Nicolette, 2015) from Manning are both insanely helpful for project tracking and presentation. The key insight is metrics can be helpful or arbitrary depending on the team leaders methodology. Below are a few of the models I've found most useful for day to day tracking and for stakeholder updates.


## Burn Charts
For linear and iterative processes, burn charts determine if the team is likely to meet the target. The straightforward metric measures the amount of effort by the team, the amount of work needed to finish, and completion rate of the team. We use burn charts for waterfall projects, but they are also valuable in agile where the lead is able to look at throughput by iteration. The biggest challenge with measuring effort is that management will want to squeeze out more effort from workers. That doesn't work and leads to burnout.

Our burn chart could have either been a burn-up chart, which tracks the cumulative documents completed, or a burn-down chart, which tracks the cumulative documents left to complete. The team used a burn-down chart as it is similar to a finish line and we had a set delivery date. The chart is simple enough. The columns are start date, end date, expected tasks remaining, actual tasks remaining. The rows are made up of sprints, and we kept it simple by listing out work weeks. 

## Insights
Burn charts give a straightforward narrative to the measured project. For this example, lets say we have 50 weeks to complete 100 documents. The expected column would simply list two documents completed each week, with a cumulative count of 100 by the end of the project at week 50. Advanced planners can adopt an efficiency ratio, but lets keep the math easy for illustrative purposes. 

This chart lets the team know if they are falling being or if they are ahead. In the case of our project, we noticed that the first few weeks listed zero documents created. We attributed this to ramp up time and learning the material. We also had zero documents created midway through the project, when the project scope changed. Listing project features against the expected timeline is a good way to get a clearer picture of hiccups in the project, and if the delivery date is still obtainable.

## Throughput
The examples here use a concept called throughput, which measures how much a team can deliver, and if its delivery is consistent. Another way of thinking of throughput is one of forecasting future delivery. A few things are necessary for this metric to be accurate. 

First, the team needs to have a realistic definition of delivered. Initially, my team thought delivered meant emailing the document to QA. But after a few back and forths and corrections later, and all of a sudden this “delivered” document was overdue by a few weeks. The team needs to agree on the definition of done. Additionally, the scope and schedule of the project should remain fixed. A change in scope can invalidate the metric in determining future work. 

Displaying metrics in this manners helped the team keep progress visible, updates stakeholders on status and kept them in the loop of future progress, and alerted the team to any patterns or hiccups that could be used to fine tune the next sprint of project. We did not measure man hours or lines of code, and instead measured completed documents because this is what we were delivering to the client. In the way, our project tracking was practical and useful for several work groups.


## Other Metrics
- Cycle Chart–This measures the consistency of a team's performance by looking at the average time needed to create a single item. Very useful for estimating the amount of work needed for future projects.


- Cumulative Flow–What are the bottlenecks in the project? Found in Kanban, this diagram can show work in progress. This is valuable for displaying current work and how delivery can be sped up. Very useful for calling out a department that is consistently slow.


A few concluding remarks: remember that new projects, workflows, and systems require a ramp-up time from employees. If you are thinking of introducing framework X, then manage stakeholder expectations and include a lower throughput of work. And lastly, these metrics and reports are conversation starters. They reveal patterns and observations, and should not be taken as concluding remarks.












