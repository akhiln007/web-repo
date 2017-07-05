---
layout: post
title: SQL - SELECT Statement for retrieving data
---
{{ page.title }}
================

The SELECT statement is used to select data from a database. The data returned is stored in a result table, called the result-set.

SELECT Syntax

SELECT column1, column2, ...
FROM table_name;

Here, column1, column2, ... are the field names of the table you want to select data from. If you want to select all the fields available in the table, use the following syntax:

SELECT * FROM table_name;

1) SELECT Column Example

The following SQL statement selects the "CustomerName" and "City" columns from the "Customers" table.

SELECT CustomerName, City FROM Customers;

2) SELECT * Example

The following SQL statement selects all the columns from the "Customers" table.

SELECT * FROM Customers;

3) SELECT DISTINCT Statement

The SELECT DISTINCT statement is used to return only distinct (different) values. Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.

The SELECT DISTINCT statement is used to return only distinct (different) values.

SELECT DISTINCT column1, column2, ...
FROM table_name;

4) SELECT Example

The following SQL statement selects all (and duplicate) values from the "Country" column in the "Customers" table:

SELECT Country FROM Customers;

5) SELECT DISTINCT Examples

The following SQL statement selects only the DISTINCT values from the "Country" column in the "Customers" table:

SELECT DISTINCT Country FROM Customers;

The following SQL statement lists the number of different (distinct) customer countries:

SELECT COUNT(DISTINCT Country) FROM Customers;

6) Defining a Column Alias

A column alias:

• Renames a column heading

• Is useful with calculations

• Immediately follows the column name (There can also be the optional AS keyword between the column name and alias.)

• Requires double quotation marks if it contains spaces or special characters, or if it is case-sensitive

SELECT last_name AS name, commission_pct comm
FROM employees;

SELECT last_name "Name" , salary*12 "Annual Salary"
FROM employees;

7) Arithmetic Expressions

Create expressions with number and date data by using arithmetic operators.

SELECT last_name, salary, salary + 300
FROM employees;

8) Defining a Null Value

Null is a value that is unavailable, unassigned, unknown, or inapplicable.Null is not the same as zero or a blank space.

SELECT last_name, job_id, salary, commission_pct
FROM employees;

9) Concatenation Operator

A concatenation operator:

• Links columns or character strings to other columns.

• Is represented by two vertical bars (||).

• Creates a resultant column that is a character expression.

SELECT last_name||job_id AS "Employees"
FROM employees;

10) Literal Character Strings

• A literal is a character, a number, or a date that is included in the SELECT statement.

• Date and character literal values must be enclosed within single quotation marks.

• Each character string is output once for each row returned.


SELECT last_name ||' is a '||job_id AS "Employee Details"
FROM employees;

11) Alternative Quote (q) Operator

Specify your own quotation mark delimiter.

• Select any delimiter.

• Increase readability and usability.

SELECT department_name || ' Department' || q'['s Manager Id: ]' || manager_id AS "Department and Manager"
FROM departments;

12) Displaying the Table Structure

• Use the DESCRIBE command to display the structure of a table.

DESCRIBE employees



