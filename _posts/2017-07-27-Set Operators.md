---
layout: post
title: SQL - Set Operators
---

{{ page.title }}
================


1) Oracle Server and Set Operators

• Duplicate rows are automatically eliminated except in UNION ALL.

• Column names from the first query appear in the result.

• The output is sorted in ascending order by default except in UNION ALL.


2) SQL UNION Operator

The UNION operator returns all rows that are selected by either query. Use the UNION operator to return all rows from multiple tables and eliminate any duplicate rows.

• Each SELECT statement within UNION must have the same number of columns.
 
• The columns must also have similar data types.

• The names of the columns need not be identical.

• NULL values are not ignored during duplicate checking.

• The columns in each SELECT statement must also be in the same order.

SELECT column_name(s) FROM table1

UNION

SELECT column_name(s) FROM table2;

SELECT 'Customer' As Type, ContactName, City, Country
FROM Customers

UNION

SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;

• Matching the SELECT Statement: Example

SELECT location_id, department_name "Department",
TO_CHAR(NULL) "Warehouse location"
FROM departments

UNION

SELECT location_id, TO_CHAR(NULL) "Department",
state_province
FROM locations;

SELECT employee_id, job_id,salary
FROM employees

UNION

SELECT employee_id, job_id,0
FROM job_history;

3) UNION ALL Syntax

Use the UNION ALL operator to return all rows from multiple queries.

Following SQL Display's the current and previous departments of all employees.

SELECT employee_id, job_id, department_id
FROM employees

UNION ALL

SELECT employee_id, job_id, department_id
FROM job_history
ORDER BY employee_id;

4) Intersect

Use the INTERSECT operator to return all rows that are common to multiple queries.

Guidelines

• The number of columns and the data types of the columns being selected by the SELECT statements in the queries must be identical in all the SELECT statements used in the query. The names of the columns, however, need not be identical.

• Reversing the order of the intersected tables does not alter the result.

• INTERSECT does not ignore NULL values.

Following SQL Display's the employee IDs and job IDs of those employees who currently have a job title that is the same as their previous one.

SELECT employee_id, job_id, department_id
FROM employees

INTERSECT

SELECT employee_id, job_id, department_id
FROM job_history;

5) MINUS Operator

Use the MINUS operator to return all distinct rows selected by the first query, but not present in the second query result set (the first SELECT statement MINUS the second SELECT statement).

Following SQl Display's the employee IDs of those employees who have not changed their jobs even once.

SELECT employee_id
FROM employees

MINUS

SELECT employee_id
FROM job_history;

6) Using the ORDER BY Clause in Set Operations

• The ORDER BY clause can appear only once at the end of the compound query.

• Component queries cannot have individual ORDER BY clauses.

• ORDER BY clause recognizes only the columns of the first SELECT query.

• By default, the first column of the first SELECT query is used to sort the output in an ascending order.


References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
