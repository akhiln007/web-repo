---
layout: post
title: SQL - Managing Schema Objects
---

{{ page.title }}
================


1) ALTER TABLE Statement

Use the ALTER TABLE statement to:

• Add a new column

ALTER TABLE dept80 ADD (job_id VARCHAR2(9));

• Modify an existing column

ALTER TABLE dept80 MODIFY (last_name VARCHAR2(30));

• Define a default value for the new column

• Drop a column

ALTER TABLE dept80 DROP COLUMN job_id;

2) SET UNUSED Option

• You use the SET UNUSED option to mark one or more columns as unused.

ALTER TABLE dept80 SET UNUSED (last_name);

• You use the DROP UNUSED COLUMNS option to remove the columns that are marked as unused.

ALTER TABLE dept80 DROP UNUSED COLUMNS;

3) Managing constraints

Use the ALTER TABLE statement to:

• Add or drop a constraint, but not modify its structure

ALTER TABLE emp2 ADD CONSTRAINT emp_mgr_fk FOREIGN KEY(manager_id) REFERENCES emp2(employee_id);

ALTER TABLE emp2 DROP CONSTRAINT emp_mgr_fk;

ALTER TABLE emp2 DROP COLUMN employee_id CASCADE CONSTRAINTS;

• Enable or disable constraints

ALTER TABLE emp2 DISABLE CONSTRAINT emp_dt_fk;

ALTER TABLE emp2 ENABLE CONSTRAINT emp_dt_fk;

• Add a NOT NULL constraint by using the MODIFY clause

• Renaming Table Columns and Constraints

ALTER TABLE marketing RENAME COLUMN team_id TO id;

4) Overview of Indexes

Indexes are created:

• Automatically

– PRIMARY KEY creation

– UNIQUE KEY creation

• Manually

– The CREATE INDEX statement

– The CREATE TABLE statement

5) CREATE INDEX with the CREATE TABLE Statement

CREATE TABLE NEW_EMP (employee_id NUMBER(6) PRIMARY KEY USING INDEX(CREATE INDEX emp_id_idx ON NEW_EMP(employee_id)),first_name VARCHAR2(20),last_name VARCHAR2(25));

SELECT INDEX_NAME, TABLE_NAME FROM USER_INDEXES WHERE TABLE_NAME = 'NEW_EMP';

OR

CREATE TABLE NEW_EMP2 (employee_id NUMBER(6), first_name VARCHAR2(20), last_name VARCHAR2(25));

CREATE INDEX emp_id_idx2 ON new_emp2(employee_id);

ALTER TABLE new_emp2 ADD PRIMARY KEY (employee_id) USING INDEX emp_id_idx2;

6) Function-Based Indexes

• A function-based index is based on expressions.

• The index expression is built from table columns, constants, SQL functions, and user-defined functions.

CREATE INDEX upper_dept_name_idx ON dept2(UPPER(department_name));

SELECT * FROM dept2 WHERE UPPER(department_name) = 'SALES';

7) Removing an Index

DROP INDEX upper_dept_name_idx;

8) DROP TABLE … PURGE

DROP TABLE dept80 PURGE;

Oracle Database provides a feature for dropping tables. When you drop a table, the database does not immediately release the space associated with the table. Rather, the database renames the table and places it in a recycle bin, where it can later be recovered with the FLASHBACK TABLE statement if you find that you dropped the table in error. If you want to immediately release the space associated with the table at the time you issue the DROP TABLE statement, then include the PURGE clause.

9) FLASHBACK TABLE Statement

• Enables you to recover tables to a specified point in time with a single statement.

• Restores table data along with associated indexes, and constraints.

• Enables you to revert the table and its contents to a certain point in time or SCN.

DROP TABLE emp2;

SELECT original_name, operation, droptime FROM recyclebin;

FLASHBACK TABLE emp2 TO BEFORE DROP;

10) External Tables

An external table is a read-only table whose metadata is stored in the database but whose data is stored outside the database. This external table definition can be thought of as a view that is used for running any SQL query against external data without requiring that the external data first be loaded into the database. The main difference between external tables and regular tables is that externally organized tables are read-only. No data manipulation language (DML) operations are possible, and no indexes can be created on them.

11) Creating a Directory for the External Table

CREATE OR REPLACE DIRECTORY emp_dir AS '/…/emp_dir';

GRANT READ ON DIRECTORY emp_dir TO hr;

12) Creating an External Table by Using ORACLE_LOADER

CREATE TABLE oldemp (fname char(25), lname CHAR(25))ORGANIZATION EXTERNAL(TYPE ORACLE_LOADERDEFAULT DIRECTORY emp_dirACCESS PARAMETERS
(RECORDS DELIMITED BY NEWLINE
NOBADFILE
NOLOGFILE
FIELDS TERMINATED BY ','
(fname POSITION ( 1:20) CHAR,
lname POSITION (22:41) CHAR))
LOCATION ('emp.dat'))
PARALLEL 5
REJECT LIMIT 200;

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
