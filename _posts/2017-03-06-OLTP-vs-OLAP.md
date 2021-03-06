---
layout: post
title: DW - OLTP vs OLAP
---

{{ page.title }}
================

1) Operational Data (OLTP Applications)

Data that “works”

For eg: for taking money from an ATM, you need to know the Bank a/c no., ATM PIN, Balance etc.

a) Frequent updates and queries.

b) Normalized for efficient search and updates.

c) Fragmented and local relevance.

d) Point Queries: queries accessing individual tuples.(eg: what are the last 10 transactions).

Example OLTP Queries:-

a) What is the salary of Mr. Nair.

b) What is the address and phone number of person in charge of the supplies department.

c) How many employees have received an ‘’excellent’’ credentials in the latest appraisal.

2) Historical Data (OLAP)

Data that “tells”

If you take all the data from all the railway reservation centers for the last 10 years. It will tell us the trends about which are the peak time in which people travel, what kind of people travel in sleeper class, A/C etc.

a) Very infrequent updates.

b) Analytical queries that requires huge amount of aggregation.

For eg: What is the average age of people travelling in sleeper class. This requires calculation for huge amount of data sets.

c) Performance issues mainly in query response time (not in updates).

Example OLAP Queries:-

a) How is the employee attrition scene changing over the years across the company.

b) Is it financially viable to continue our manufacturing unit in Kerala.

3) Datawarehouse

a) An infrastructure to manage historical data.

b) Designed to support OLAP queries involving use of aggregates.

c) Post retrieval processing(reporting).

4) Datamart

Data warehouses are seen as a collection of data marts - Or  historical data about each OLTP segment/module that feeds into the Datawarehouse.

5) OLAP Query Characteristics

a) Aggregation and summarization over large data sets.

b) Trend detection.

c) Multi- dimensional projections.

6) ROLAP

In ROLAP, the hypercube queries are transformed to relational queries and maintain the data cube in a set of RDBMS tables.

7) MOLAP

Use a separate storage model for multi dimensional data.
