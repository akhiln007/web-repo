---
layout: post
title: SQL - Managing Objects with Data Dictionary Views
---

{{ page.title }}
================

1) Data Dictionary

User tables are tables created by the user and contain business data, such as EMPLOYEES. There is another collection of tables and views in the Oracle database known as the data dictionary. This collection is created and maintained by the Oracle server and contains information about the database.

• USER_OBJECTS

• USER_TABLES

• USER_TAB_COLUMNS

2) Data Dictionary Structure

View naming convention:

• USER : User’s view (what is in your schema; what you own)

• ALL  : Expanded user’s view (what you can access)

• DBA  : Database administrator’s view (what is in everyone’s schemas)

• V$   : Performance-related data

3) How to Use the Dictionary Views

• Start with DICTIONARY. It contains the names and descriptions of the dictionary tables and views.

• DESCRIBE DICTIONARY

• SELECT * FROM dictionary WHERE table_name = 'USER_OBJECTS';

4) USER_OBJECTS and ALL_OBJECTS Views

• USER_OBJECTS:

Query USER_OBJECTS to see all the objects that you own.

• ALL_OBJECTS:

Query ALL_OBJECTS to see all objects to which you have access.

5) Table Information

USER_TABLES:

• DESCRIBE user_tables

• SELECT table_name FROM user_tables;

6) Column Information

USER_TAB_COLUMNS:

• DESCRIBE user_tab_columns;

• SELECT column_name, data_type, data_length,data_precision, data_scale, nullable FROM user_tab_columns WHERE table_name='EMPLOYEES';

7) Constraint Information

• USER_CONSTRAINTS describes the constraint definitions on your tables.

• USER_CONS_COLUMNS describes columns that are owned by you and that are specified in constraints.

• DESCRIBE user_constraints;

• SELECT constraint_name, constraint_type,search_condition, r_constraint_name,delete_rule, status FROM user_constraints WHERE table_name = 'EMPLOYEES';

8) Querying USER_CONS_COLUMNS

• DESCRIBE user_cons_columns;

• SELECT constraint_name, column_name FROM user_cons_columns WHERE table_name = 'EMPLOYEES';

9) View Information

• DESCRIBE user_views

• SELECT DISTINCT view_name FROM user_views;

• SELECT text FROM user_views WHERE view_name = 'EMP_DETAILS_VIEW';

10) Sequence Information

• DESCRIBE user_sequences;

• SELECT sequence_name, min_value, max_value,increment_by, last_number FROM user_sequences;

11) Index Information

• USER_INDEXES provides information about your indexes.

• USER_IND_COLUMNS describes columns comprising your indexes and columns of indexes on your tables.

• DESCRIBE user_indexes;

• SELECT index_name, table_name,uniqueness FROM user_indexes WHERE table_name = 'EMPLOYEES';

• SELECT INDEX_NAME, TABLE_NAME FROM USER_INDEXES WHERE TABLE_NAME = 'EMP_LIB';

• DESCRIBE user_ind_columns

• SELECT INDEX_NAME, COLUMN_NAME,TABLE_NAME FROM user_ind_columns WHERE INDEX_NAME = 'LNAME_IDX';

12) Synonym Information

• DESCRIBE user_synonyms

• SELECT * FROM user_synonyms;

13) Adding Comments to a Table

• You can add comments to a table or column by using the COMMENT statement:

COMMENT ON TABLE employees IS 'Employee Information';


References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
