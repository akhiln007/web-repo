---
layout: post
title: SQL - Creating Other Schema Objects
---

{{ page.title }}
================

1) What Is a View

A view is a logical table based on a table or another view. A view contains no data of its own, but is like a window through which data from tables can be viewed or changed. The tables on which a view is based are called base tables. The view is stored as a SELECT statement in the data dictionary.

2) Advantages of Views

• Views restrict access to the data because it displays selected columns from the table.

• Views can be used to make simple queries to retrieve the results of complicated queries.

• One view can be used to retrieve data from several tables.

• Views provide groups of users access to data according to their particular criteria.

3) Simple Views and Complex Views

There are two classifications for views: simple and complex. The basic difference is related to the DML (INSERT, UPDATE, and DELETE) operations.

A simple view is one that:

- Derives data from only one table

- Contains no functions or groups of data

- Can perform DML operations through the view

• A complex view is one that:

- Derives data from many tables

- Contains functions or groups of data

- Does not always allow DML operations through the view

4) Creating a View

You embed a subquery in the CREATE VIEW statement:

CREATE [OR REPLACE] [FORCE|NOFORCE] VIEW view [(alias[, alias]...)]
AS subquery
[WITH CHECK OPTION [CONSTRAINT constraint]]
[WITH READ ONLY [CONSTRAINT constraint]];

• The subquery can contain complex SELECT syntax.

CREATE VIEW empvu80
AS SELECT employee_id, last_name, salary
FROM employees
WHERE department_id = 80;

5) Modifying a View

Modify the EMPVU80 view by using a CREATE OR REPLACE VIEW clause. Add an alias for each column name:

CREATE OR REPLACE VIEW empvu80
(id_number, name, sal, department_id)
AS SELECT employee_id, first_name || ' '
|| last_name, salary, department_id
FROM employees
WHERE department_id = 80;

• Column aliases in the CREATE OR REPLACE VIEW clause are listed in the same order as the columns in the subquery.

6) Creating a Complex View

Create a complex view that contains group functions to display values from two tables:

CREATE OR REPLACE VIEW dept_sum_vu
(name, minsal, maxsal, avgsal)
AS SELECT d.department_name, MIN(e.salary),
MAX(e.salary),AVG(e.salary)
FROM employees e JOIN departments d
ON (e.department_id = d.department_id)
GROUP BY d.department_name;

7) Rules for Performing DML Operations on a View

You can usually perform DML operations on simple views.

• You cannot remove a row if the view contains the following:

– Group functions

– A GROUP BY clause

– The DISTINCT keyword

– The pseudocolumn ROWNUM keyword

8) Denying DML Operations

• You can ensure that no DML operations occur by adding the WITH READ ONLY option to your view definition.

• Any attempt to perform a DML operation on any row in the view results in an Oracle server error.

CREATE OR REPLACE VIEW empvu10
(employee_number, employee_name, job_title)
AS SELECT employee_id, last_name, job_id
FROM employees
WHERE department_id = 10
WITH READ ONLY ;

9) Sequences

• Can automatically generate unique numbers

• Is a shareable object

• Can be used to create a primary key value

• Replaces application code

• Speeds up the efficiency of accessing sequence values when cached in memory

CREATE SEQUENCE sequence
[INCREMENT BY n]
[START WITH n]
[{MAXVALUE n | NOMAXVALUE}]
[{MINVALUE n | NOMINVALUE}]
[{CYCLE | NOCYCLE}]
[{CACHE n | NOCACHE}];

10) Creating a Sequence

• Create a sequence named DEPT_DEPTID_SEQ to be used for the primary key of the DEPARTMENTS table.

• Do not use the CYCLE option.

CREATE SEQUENCE dept_deptid_seq
INCREMENT BY 10
START WITH 120
MAXVALUE 9999
NOCACHE
NOCYCLE;

11) NEXTVAL and CURRVAL Pseudocolumns

• NEXTVAL returns the next available sequence value. It returns a unique value every time it is referenced, even for different users.

• CURRVAL obtains the current sequence value.

• NEXTVAL must be issued for that sequence before CURRVAL contains a value.

12) Using a Sequence

• Insert a new department named “Support” in location ID 2500:

INSERT INTO departments(department_id,
department_name, location_id)
VALUES (dept_deptid_seq.NEXTVAL,
'Support', 2500);

• View the current value for the DEPT_DEPTID_SEQ sequence:

SELECT dept_deptid_seq.CURRVAL FROM dual;

13) Modifying a Sequence

• Change the increment value, maximum value, minimum value, cycle option, or cache option:

ALTER SEQUENCE dept_deptid_seq
INCREMENT BY 20
MAXVALUE 999999
NOCACHE
NOCYCLE;

14) Indexes

An index:

• Is a schema object

• Can be used by the Oracle server to speed up the retrieval of rows by using a pointer

• Can reduce disk input/output (I/O) by using a rapid path access method to locate data quickly

• Is independent of the table that it indexes

• Is used and maintained automatically by the Oracle server

15) How Are Indexes Created

• Automatically: A unique index is created automatically when you define a PRIMARY KEY or UNIQUE constraint in a table definition.

• Manually: Users can create nonunique indexes on columns to speed up access to the rows.

16) Creating an Index

• Create an index on one or more columns:

CREATE [UNIQUE][BITMAP]INDEX index ON table (column[, column]...);

• Improve the speed of query access to the LAST_NAME column in the EMPLOYEES table:

CREATE INDEX emp_last_name_idx ON employees(last_name);

17) Removing an Index

• Remove the emp_last_name_idx index from the data dictionary:

DROP INDEX emp_last_name_idx;

18) Creating a Synonym

Simplify access to objects by creating a synonym (another name for an object). With synonyms, you can:

• Create an easier reference to a table that is owned by another user

• Shorten lengthy object names

CREATE [PUBLIC] SYNONYM synonym FOR object;

19) Creating and Removing Synonyms


• Create a shortened name for the DEPT_SUM_VU view:

CREATE SYNONYM d_sum FOR dept_sum_vu;

• Drop a synonym:

DROP SYNONYM d_sum;

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
