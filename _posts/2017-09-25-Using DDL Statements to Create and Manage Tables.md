---
layout: post
title: SQL - Using DDL Statements to Create and Manage Tables
---

{{ page.title }}
================

1) CREATE TABLE Statement

You create tables to store data by executing the SQL CREATE TABLE statement. This statement is one of the DDL statements that are a subset of the SQL statements used to create, modify, or remove Oracle database structures.

CREATE TABLE dept(deptno NUMBER(2),dname VARCHAR2(14),loc VARCHAR2(13),create_date DATE DEFAULT SYSDATE);

2) Referencing Another User’s Tables

• Tables belonging to other users are not in the user’s schema.

• You should use the owner’s name as a prefix to those tables.

if there are schemas named USERA and USERB, and both have an EMPLOYEES table, then if USERA wants to access the EMPLOYEES table that belongs to USERB, USERA must prefix the table name with the schema name:

SELECT * FROM userb.employees;

If USERB wants to access the EMPLOYEES table that is owned by USERA, USERB must prefix the table name with the schema name:

SELECT * FROM usera.employees;

3) DEFAULT Option

• Specify a default value for a column during an insert.

• Literal values, expressions, or SQL functions are legal values.

• Another column’s name or a pseudocolumn are illegal values.

• The default data type must match the column data type.

CREATE TABLE hire_dates(id NUMBER(8),hire_date DATE DEFAULT SYSDATE);

4) Data Types

• VARCHAR2(size):- Variable-length character data

• CHAR(size):- Fixed-length character data

• NUMBER(p,s):- Variable-length numeric data

• DATE:- Date and time values

• LONG:- Variable-length character data (up to 2 GB)

• CLOB:- Character data (up to 4 GB)

• RAW and LONG RAW:- Raw binary data

• BLOB:- Binary data (up to 4 GB)

• BFILE:- Binary data stored in an external file (up to 4 GB)

• ROWID:- A base-64 number system representing the unique address of a row in its table

5) Datetime Data Types

TIMESTAMP:- Date with fractional seconds

INTERVAL YEAR TO MONTH:- Stored as an interval of years and months

INTERVAL DAY TO SECOND:- Stored as an interval of days, hours, minutes,and seconds

6) Including Constraints

• Constraints enforce rules at the table level.

• Constraints prevent the deletion of a table if there are dependencies.

• The following constraint types are valid:

– NOT NULL

– UNIQUE

– PRIMARY KEY

– FOREIGN KEY

– CHECK

7) Defining Constraints

• Example of a column-level constraint:

CREATE TABLE employees(employee_id NUMBER(6) CONSTRAINT emp_emp_id_pk PRIMARY KEY,first_name VARCHAR2(20),...);

• Example of a table-level constraint:

CREATE TABLE employees(employee_id NUMBER(6),first_name VARCHAR2(20),...job_id VARCHAR2(10) NOT NULL,CONSTRAINT emp_emp_id_pk PRIMARY KEY (EMPLOYEE_ID));

8) NOT NULL Constraint

Ensures that null values are not permitted for the column. NOT NULL constraints must be defined at the column level.

9) UNIQUE Constraint

A UNIQUE key integrity constraint requires that every value in a column or a set of columns (key) be unique—that is, no two rows of a table can have duplicate values in a specified column or a set of columns. UNIQUE constraints can be defined at the column level or table level.

CREATE TABLE employees(
employee_id NUMBER(6),
last_name VARCHAR2(25) NOT NULL,
email VARCHAR2(25),
salary NUMBER(8,2),
commission_pct NUMBER(2,2),
hire_date DATE NOT NULL,
...
CONSTRAINT emp_email_uk UNIQUE(email));


10) PRIMARY KEY Constraint

A PRIMARY KEY constraint creates a primary key for the table. Only one primary key can be created for each table. The PRIMARY KEY constraint is a column or a set of columns that uniquely identifies each row in a table.

11) FOREIGN KEY Constraint

The FOREIGN KEY (or referential integrity) constraint designates a column or a combination of columns as a foreign key and establishes a relationship with a primary key or a unique key in the same table or a different table.
Defined at either the table level or the column level.

CREATE TABLE employees(
employee_id NUMBER(6),
last_name VARCHAR2(25) NOT NULL,
email VARCHAR2(25),
salary NUMBER(8,2),
commission_pct NUMBER(2,2),
hire_date DATE NOT NULL,
...
department_id NUMBER(4),
CONSTRAINT emp_dept_fk FOREIGN KEY (department_id)
REFERENCES departments(department_id),
CONSTRAINT emp_email_uk UNIQUE(email));

• FOREIGN KEY: Defines the column in the child table at the table-constraint level.

• REFERENCES: Identifies the table and column in the parent table.

• ON DELETE CASCADE: Deletes the dependent rows in the child table when a row in the parent table is deleted.

• ON DELETE SET NULL: Converts dependent foreign key values to null.

12) CHECK Constraint

• Defines a condition that each row must satisfy

• The following expressions are not allowed:

– References to CURRVAL, NEXTVAL, LEVEL, and ROWNUM pseudocolumns

– Calls to SYSDATE, UID, USER, and USERENV functions

– Queries that refer to other values in other rows

13) Creating a Table Using a Subquery

• Create a table and insert rows by combining the CREATE TABLE statement and the AS subquery option.

• Match the number of specified columns to the number of subquery columns.

• Define columns with column names and default values.

CREATE TABLE dept80
AS
SELECT employee_id, last_name,
salary*12 ANNSAL,
hire_date
FROM employees
WHERE department_id = 80;

14) ALTER TABLE Statement

Use the ALTER TABLE statement to:

• Add a new column

• Modify an existing column definition

• Define a default value for the new column

• Drop a column

• Rename a column

• Change table to read-only status

15) Read-Only Tables

Use the ALTER TABLE syntax to put a table into the read-only mode:

• Prevents DDL or DML changes during table maintenance

• Change it back into read/write mode

ALTER TABLE employees READ ONLY;

ALTER TABLE employees READ WRITE;

16) Dropping a Table

• Moves a table to the recycle bin.

• Removes the table and all its data entirely if the PURGE clause is specified.

• Invalidates dependent objects and removes object privileges on the table.

DROP TABLE dept80;

