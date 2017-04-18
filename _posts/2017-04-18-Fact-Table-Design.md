---
layout: post
title: DW - Fact Table Design
---

{{ page.title }}
================

1) Logical Model

A fact table is the primary table in a dimensional model where the numerical performance measurements of the business are stored. 
A fact table also expresses the many-to-many relationships between dimensions in dimensional models.

In Fact table design document, the following design points should be captured:

- Provide the lowest level of detail data.
- Create a grain statement.
- Identify Dimensions.
- Define Types of Fact Table.
- Define Facts.
- Define Calculations.
- Multi Currency requirement for monetary measures.
- Multi Unit-of-Measure requirement for quantity measures.

2) Define Fact Grain

Defining the grain is the most important step when designing a fact table as grain determines the level of detail; it tells how you 
describe a single row in the fact table. In general, the lowest level of information associated with a business process should be 
defined for maximum flexibility.

For each fact table, a fact grain statement should be included in the design.

Fact grain statement example: 

- Each Purchase Order distribution.
- Daily inventory snapshot.
- Each Invoice Line distribution.
- Each Sales Opportunity Product Line.
- Monthly payroll line for each employee.

3) Define Fact Table Type

Kimball defined three types of fact table in dimensional model: Transaction Fact, Period Snapshot fact and Accumulated Snapshot. 
Each fact table type has its characteristics and data populating mechanism.Understanding the type of fact table facilitates metrics 
selection and decreases confusion in BI reporting.

4) Define Facts

Fact represents a business measure. The most useful facts are numeric and additive, such as Sales Order Amount, Head Count.  
Three types of facts(Additive, Semi-Additive amd Non-Additive) can be determined based on its additive nature.

Kimball Tips: Transactions and snapshots are the yin and yang of dimensional data warehouse. Used together, companion transaction and 
snapshot fact tables provide a complete view of the business. We need both because there is often no simple way to combine these two 
contrasting perspectives.

5) Define Calculations

Facts are measured, “continuously valued”, rapidly changing information. They can be calculated and/or derived. Base fact usually is 
designed as a fact column e.g. Journal Amount, Budget Amount, derived fact can be a fact column or be defined in BI tool metadata, 
e.g. Budget Variance Amount is the difference between Journal Amount and Budget Amount.

Calculation formula for a derived fact should be detail specified in the design document.

6) Physical Model :Transaction Fact Table

Kimball Tips: Transaction data often is structured quite easily into a dimensional framework the lowest level data is the most 
naturally dimensional data, supporting analyses that cannot be done on summarized data. Transaction-level data let us analyze behavior 
in extreme detail.

7) Physical Model: Snapshot Fact Table

Kimball Tips: The periodic snapshot fact table often is the only place to easily retrieve a regular, predictable, trendable view 
of the key business performance metrics.

8) Physical Model: Consolidated Fact Table

Combine frequently used metrics from different business processes into a consolidated table for query performance if possible. 
When joining two fact tables together, be very careful of the fact tables of different granularity. Use multipass SQL code to 
query each fact table in separate queries and then outer join the two answer sets when populating the consolidated fact. 
The multipass approach has additional benefits in terms of better query performance.

Example of consolidated fact: 

- Spend analyzer uses data from Purchase Order business process and AP Invoice business process, while each of these two business 
processes owns a transaction fact, the cross business analysis can be queries through a consolidated fact table. 

- Financial has a GL Journal Ledger Summary fact that takes data from GL Budget fact (a transaction fact) and GL journal entry line 
fact (a transaction fact).

- Human Resources Intelligence has a Turnover fact which merges Headcount data (a snapshot fact) and Job data (a transaction fact). 

- Inventory Balance analysis includes metrics from Inventory Balance Fact (a snapshot fact) and Inventory COGS fact (a transaction fact). 

- A consolidated fact can have the combination of two transaction facts (Spend Analyzer), transaction and snapshot fact (HR Turnover), 
or two snapshot facts. 

Kimball Tips: If users are frequently combining data from multiple business processes, then an additional fact table can be constructed 
that combines the data once into a second-level, consolidated fact table rather than relying on users to combine the data consistently
and accurately on their own.

9) Physical Model: Factless Fact Table

Factless fact tables record either coverage or the occurrence of an event, e.g. Class Attendance, Workforce Snapshot, 
Insurance Accident Fact. As the name suggests, factless fact tables do not have numeric metrics. A counter or an indicator with the 
value of 1 or 0 can be added to each fact record to facilitate counting.

10) Physical Model: Fact Table Aggregation

Fact Aggregation refers to summarized fact table records derived from base-level fact tables. Aggregate (summary) records are a 
very effective tool for performance tuning in a large data warehouse. However, there’s a trade-off between enhanced query performances 
versus additional backroom maintenance headache. Aggregations are a performance-tuning vehicle. As with indices, aggregated 
fact tables should be monitored and adjusted periodically.

It is impractical to build all potential aggregation combinations. If a simple fact table containing five dimensions and each 
dimension has two additional attributes that are candidates for aggregation, there are 125 different potential aggregate fact tables!

Aggregation considerations:

- Understand usage patterns to improve performance for majority of the queries.
- Business requirement analysis: what data are being queried most frequently?
- On-going monitoring: user access pattern analysis.
- Understand data compression
- A statistical distribution of the data can be helpful.
- Look for minimum of 50:1 or even higher detail-to-summary ratio.

Although more fact and dimension tables will be created, it is recommended separating base and aggregated tables:

- Separate table can have different partition access for better performance
- Table administration for loading, indexing is easier
- Maintain single grain in fact table minimizes risk of double-counting user error.
- OBIEE aggregation awareness feature which leverages usage statistics allows BI engine accessing the most appropriate aggregated 
table for best query performance
- Accessing base vs. aggregate table is transparent to users in OBIEE.

It is also recommended to develop a list of initial aggregations right after finish modeling when user’s requirements are still fresh
in memory. Do not create aggregation unless it is absolutely necessary. Consider query performance versus maintenance.

Kimball Tips: Given the stringent rules about mixing fact table granularity, each distinct fact table aggregation should occupy its 
own physical fact table.

11) Physical Model: Multi-Currency in Fact Table

To support Multi-Currency requirement in Fusion BI, each currency code should be defined in four currency columns: Transaction Currency,
Base Currency (aka. Functional Currency), First Alternate Reporting Currency, and Second Alternate Reporting Currency. Each monetary 
amount field should be defined in four amount columns representing correspondent currency code.

12) Physical Model: Unit of Measure in Fact Table

To support consistent representation of source quantities data in various UOM, both Source Unit of Measure code and Data Warehouse 
Unit of Measure code should be defined in the fact table. Quantity fields also need to be defined in two columns representing the 
corresponding UOM. 
