---
layout: post
title: DW - Dimension Design
---

{{ page.title }}
================


To start data warehouse Dimension design, we begin with Logical model. A logical model represents data in purely business terms. Before 
physical model starts, the modeler should have logical model reviewed and acknowledged by the business user. 

Dimension logical modeling can use Adapt (Application Design for Analytical Processing Technologies) OLAP objects for Microsoft Visio 
software. Free download the Adapt OLAP objects shape from its website to Visio directory.  (www.symcorp.com)

1)	Logical Model 

Dimension logical model includes Dimension scope, hierarchy, level and dimension attribute.

1.1)	Dimension Scope

Scope is the collection of dimension members 

e.g. Customer, Bill-to-Customer, Ship-to-Customer, Service Customer, Industry, Customer Geography, Customer Account are all in the scope of Customer Dimension. 

Another example will be Day, Week, Month, Year, Hours, Minute, Second are all in Time Dimension Scope. Scope allows us to create a subset of information.
		
1.2)	Dimension Hierarchy

Hierarchy is the set of parent/child member combinations that define roll up relationship and aggregation. It is generally made 
up of levels.
	
1.3)	Dimension Level
	
Level is a collection of dimension members used to define hierarchical precedence. A level could point back to itself which makes the 
hierarchy become a value based hierarchy, aka recursive hierarchy or rugged hierarchy, 

e.g. Manager Hierarchy, Product Category hierarchy.
	
1.4)	Dimension Attribute

Attributes are the descriptive information about the members of a dimension. Most attributes are of character data type, they could 
also be numeric.

e.g. Product Price, Number of Work days.

Analytics benefit most from a robust set of dimension attributes, a Customer dimension or Product dimension could easily hold more 
than 100 attributes for an in-depth Customer and Product analysis.
