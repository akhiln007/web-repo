---
layout: post
title: DW - Dimension Design Consideration
---

{{ page.title }}
================

1) Surrogate Key

A system generated incremental integer, aka Surrogate Key, is recommended in the dimension. Surrogate key is used to:

- Isolate data warehouse from operational data changes.

- Smaller keys translate into smaller fact tables and smaller fact table indices and more fact table rows per block I/O.

- Allows data integration of multiple operational source.

- Provide mechanism for Slow Changing Dimension.

- Handle “Unassigned” and “Missing” dimension data.

- Increase BI query performance by easily join fact and dimension table using integer field.
	
Kimball Tips: Every join between dimension and fact tables in the data warehouse should be based on meaningless integer surrogate key. You should avoid using the natural operational production codes. None of the data warehouse keys should be smart, where you can tell something about the row just by looking at the key.


2) Star Schema 

  Star Schema is the most natural way to model a data warehouse, where only one join establishes the relationship between the fact table and any one of the dimension tables. Although OBIEE tool supports both Star Schema and Snowflake Schema, Star schema is recommended for data modeling. Fact tables in either star or snowflake schema is identical, however, the dimension tables are modeled differently. 

Why star schema?

- Dimension data are denormalized into flat table design. 

- Central Fact Table.

- Less tables are created for Dimension.

- Optimize query performance by reducing chains of joins.

- Small metadata (Few FK’s needs to be stored).

- Simple to comprehend and design.

- Data warehouse best practice.

Oracle Database Data Warehousing Guide: Oracle recommends that you choose a star schema unless you have a clear reason not to.


3)	Permissible Snowflake

  The snowflake schema is a variation of the star schema in which the redundant attributes are removed from the dimension tables and placed in normalized tables.
  
- Central Fact table.

- Normalized dimension tables storing atomic data units.

- Faster query responses.

- Easy Updation.

Limitations	

  - Large amount of meta-data.

	- May result in too many tables.

	- Harder to comprehend manually.

There are scenarios that snowflake schema could be useful:	

- When hierarchy levels or attributes are used in various fact aggregation. If an Order Fact is captured at the Product level, it should use Product Dimension. If the Order fact is also aggregated at Product Group level for query performance, a Product Group Dimension should be created.

- When levels in hierarchy constitutes a recursive hierarchy.	

- When dimension attributes can be enriched from external source.

- 3rd party system can provide rich attributes to data warehouse dimensions, e.g. Dun and Bradstreet Rating Data. Usually these data are sourced from external system and can be loaded to data warehouse at different time or at different frequency. It is more efficient to model 3rd party attributes data in a separate table and provides the link to main dimension table.

4)	Slow Changing Dimension

Slow changing dimension refers to the dimension whose attributes evolve over time, e.g. Persons change their names, work location, job code etc.  For every slow changing dimension attributes, it needs to identify “change” history.

	Depending on business requirement, a slow changing dimension can be designed in three basic options:
  
  Type 1 SCD
  
  Handling: Overwrite the Changed Attribute value.
  Advantage:	Easy and fast
  Disadvantage:	Lose history of changes
  
  Type 2 SCD
  
  Handling: Add a new Dimension Record.
  Advantage:	Reflect history.
  Disadvantage:		Dimension table growth; Requires Surrogate key.
  
  Type 3 SCD
  
  Handling: Add a new column for prior attribute.
  Advantage:	Before and after views.
  Disadvantage:		Lose intermediate values.
  
  A recap of Type 2 SCD processing (from Kimball Design Tips)

  Suppose that an individual employee changes office location, affecting the values of five attributes in the employee record. Here are the steps for what we call Type 2 SCD processing:
 
  - Create a new employee dimension record with the next surrogate key (adding 1 to the highest key value previously used). Copy all the fields from the previous most-current record, and change the five office location fields to the new values.

  - Set the change date to today, the begin-effective date-time to now, the end-effective date-time to December 31, 9999 11:59 pm, the change reason to “Relocation”, and the most recent flag to True.

  - Update the end-effective date-time of the previously most-current record for that employee to now minus 1 second, and change the most recent flag to False.

  - Begin using the new surrogate key for that employee in all subsequent fact table record entries.

5) Degenerate Dimension

A degenerate dimension (DD) acts as a dimension key in the fact table, however, it does not join to a corresponding dimension table. Degenerate dimensions commonly occur when the fact table’s grain is a single transaction.

Keep operational control numbers such as order numbers, invoice numbers in fact table and use it as degenerate dimension. Degenerate dimensions often play an integral role in the fact table’s primary key. Instead of combining all foreign keys in fact table (e.g. surrogate key columns) for primary key, the degenerate dimension guarantees the uniqueness of a fact table row. Degenerate dimension is a good candidate for fact record counts. 

Kimball Tips: We typically do not implement a surrogate key for DD. Usually the values for the degenerate dimension are unique and reasonably sized. However, if the operational identifier is an unwieldy alpha-numeric, a surrogate key might conserve significant space, especially if the fact table has a large number of rows.

6)	Role-Playing Dimension

Role playing occurs when a single physical dimension table appears several times in a fact table, each represented as a separate logical table. E.g. Order Date Dimension, Purchase Date Dimension, Service Date Dimension, Hire Date Dimension can all be sourced from Time Date Dimension. Do not create multiple physical tables for all Time Date related dimension, instead, a database view or OBIEE view can be created from the role playing Date dimension.

Kimball Tips: Role-playing in a data warehouse occurs when a single dimension simultaneously appears several times in the fact table. The underlying dimension may exist as a single physical table, but each of the roles should be presented to the data access tools in a separately labeled view.

7)	Junk Dimensions

Instead of storing multiple indicators and flags in the fact table, they could be grouped together to form a junk dimension.

Kimball Tips: A junk dimension is a convenient grouping of typically low-cardinality flags and indicators. By creating an abstract dimension, we remove the flags from the fact table while placing them into a useful dimensional framework.
	 

8)	Rolled-up Dimension

Rolled-up Dimension refers to the dimension that is created from the base dimension table. It is used strictly for aggregated fact. As we do not need to build all potential aggregation combination of a fact table, neither do we need to create all levels of base dimension into rolled-up dimension tables.

Rolled-up Dimension has its own surrogate key and need to carry attributes for its level from base dimension. Consider Rolled-up dimension as an independent dimension table.

Kimball Tips: When aggregating facts, we either eliminate dimensionality or associate the facts with a roll-up dimension. These rolled-up, aggregated dimension tables should be shrunken versions of the dimension associated with the granular base fact table. In this way, aggregated dimension conform to the base dimension table.

Note: Slow changing is a business requirement, before making a dimension into a SCD; confirm the needs with business user as slow changing dimension could have performance impact on both ETL job and BI query. 

  
  
