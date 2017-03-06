Operational Data (OLTP Applications)

-Data that “works”

For eg: for taking money from an ATM, you need to know the Bank a/c no., ATM PIN, Balance etc.

- Frequent updates and queries
- Normalized for efficient search and updates.
- Fragmented and local relevance
- Point Queries: queries accessing individual tuples.(eg: what are the last 10 transactions)

Example OLTP Queries:-

-What is the salary of Mr. Nair
-What is the address and phone number of person in charge of the supplies department.
-How many employees have received an ‘’excellent’’ credentials in the latest appraisal.


Historical Data(OLAP)

-Data that “tells”

If you take all the data from all the railway reservation centers for the last 10 years. It will tell us the trends about which are the peak time in which people travel, what kind of people travel in sleeper class, A/C etc.

-Very infrequent updates.
-Analytical queries that requires huge amount of aggregation.
For eg: What is the average age of people travelling in sleeper class. This requires calculation for huge amount of data sets.
-Performance issues mainly in query response time (not in updates).

Example OLAP Queries:-

-How is the employee attrition scene changing over the years across the company.
- Is it financially viable to continue our manufacturing unit in Kerala.

Datawarehouse

-An infrastructure to manage historical data.
-Designed to support OLAP queries involving use of aggregates.
-Post retrieval processing(reporting)

Datamart

-Data warehouses are seen as a collection of data marts - Or  historical data about each OLTP segment/module that feeds into the Datawarehouse.


OLAP Query Characteristics

-Aggregation and summarization over large data sets.
-Trend detection.
-Multi- dimensional projections.

ROLAP

In ROLAP, the hypercube queries are transformed to relational queries and maintain the data cube in a set of RDBMS tables.

MOLAP

Use a separate storage model for multi dimensional data.
