---
layout: post
title: DW - Physical Dimension Objects
---

{{ page.title }}
================

Base Table

The base level dimension is the lowest level of a dimension. It is the entry point to all levels, hierarchies and attributes of a 
dimension.

Language Table

To support multi language, a separate language outrigger table is created to supplement the language requirement for Dimension table 
that has translated description fields.

Hierarchy Table

There are two kinds of hierarchy:

1.	Level based hierarchy, e.g. Location -> City -> State -> Country -> Region.

2.	Value based hierarchy, e.g. Commodity Code -> Commodity Code Level 4   -> Commodity Code Level 3 -> Commodity Code Level 2 -> Commodity Code Level 1.

Hierarchy defined as level-based is recommended to use star schema design that is, defining all level information within the base 
dimension.Hierarchy defined as value-based, a.k.a. rugged hierarchy, recursive hierarchy should use the hierarchy helper table.

Bridge Table

Use bridge table to support multi –to – multi relationship between Dimensions or Attributes. For Example: a product can have multiple 
colors; a color may belong to multiple products.

Dimension Index

Surrogate key is the unique index for a Dimension if _SID is used. Business Key(s) in dimension table should be the primary index for a 
Dimension.

BIT MAP INDEX

 - Used on fields that are sparse (ie has only a small number of values. Eg: gender, grade etc)
 - A bit vector enumerates all possible values and sets corresponding bit for each data element.
 - Much more compact than other index structures.
 - Useful for efficiently answering composite queries over multiple bit vectored fields.
 - Can be integrated with tree index.
