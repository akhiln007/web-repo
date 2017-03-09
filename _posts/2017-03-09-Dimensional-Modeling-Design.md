---
layout: post
title: DW - Dimensional Modeling Design
---

{{ page.title }}
================

1) Consideration

Dimensional data modeling is architected to balance the data warehouse design considerations – Query Performance, Business Requirement 
and Data Warehouse maintenance. A complex data model may not perform in BI query causing long wait on the front end, a simplified
design may not meet all business requirements and large amount of data objects presented in data warehouse could become a maintenance 
headache down the road.

2) Steps  

Ralph Kimball in his “The Data Warehouse Toolkit” book recommended four steps in dimensional modeling:

a) Identify Business Process 

Dimensional data modeling starts from identifying business processes in the organization where data is being collected, e.g., Sales Order Processing in Order Management Area, Hiring Processing in Human Resource, Service Request Processing from Customer Relationship Management. The first step will decide what business processes to model by combining an understanding of the business requirements with an understanding of the available data.

One or more fact tables maybe built to support data from different business processes.

Kimball Tips: The first dimensional model built should be the one with the most impact- it should answer the most pressing business questions and be readily accessible for data extraction.

b) Identify Grain 

Determine the level of detail represented in the business process. This is how you will describe a single row in the fact table. You should start with the lowest level of information associated with a business process for maximum flexibility .e.g. Procurement process captures data at the Purchase Order level as well as Purchase Order Line level, furthermore, the data goes even lower to the Purchase Line Distribution level. 

Identifying data grain could be the most challenging task in dimensional data modelling.

Kimball Tips: Preferably you should develop dimensional models for the most atomic information captured by a business process. Atomic data is the most detailed information collected; such data cannot be subdivided further.

c) Identify Dimensions

Dimensions or their attributes are often the “By” words used to describe analytical requirements, E.g. Sales data by Customer by Product by Region. Each dimension could be thought of as an analytical “entry” point to the facts. Since operational system runs on IDs and codes, strive to convert them with verbose business language. Descriptive columns provide more business sense to the end users.

Kimball Tips: A grain statement determines the primary dimensionality of the fact table. It is often possible to add more dimensions to the basic grain of the fact table, if the additional dimension violates the grain by causing additional fact rows to be generated, then the grain statement must be revised to accommodate this dimension.

d) Identify Facts

The term fact represents a business measurement. A measurement is taken at the intersection of all the dimensions. The most useful facts are numeric and additive, such as Order Amount. Semi additive facts.

e.g., inventory balance, can be added only along some of the dimensions, and non additive facts, e.g., stock quote, discount rate, simply can’t be added at all.
  
3) Logical vs. Physical modeling

Logical modeling can be thought of as a transformer that converts business requirements into technical implementations. It helps ensure a focus on solving the business needs, regardless of the advantage or shortcomings of a particular implementation platform. 

A physical model interprets the logical model based on the strengths and weaknesses of the chosen software and hardware platforms. It is used to create the database schema.

In data warehouse development, logical model acts as the translation layer, the business perspectives are translated into dimension, hierarchy, level and attributes, the business measurements turn into key business performance indicators and metrics. Logical modeling should take place before the physical architecture is chosen.

In OBIEE term, logical model is the basis for OBIEE Business Model and Mapping Layer and physical model is for OBIEE physical layer mapping.


