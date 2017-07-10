---
layout: post
title: SQL - Restricting Data
---

{{ page.title }}
================

SQL: Restricting Data


1) The SQL WHERE Clause

The WHERE clause is used to filter records. The WHERE clause is used to extract only those records that fulfil a specified condition.Character strings and date values are enclosed with 
single quotation marks. Character values are case-sensitive and date values are format-sensitive.

SELECT column1, column2, ...
FROM table_name
WHERE condition;

SELECT last_name, job_id, department_id
FROM employees
WHERE last_name = 'Whalen' ;

SELECT last_name
FROM employees
WHERE hire_date = '17-FEB-96' ;


2) Substitution Variables

Use substitution variables to:

Temporarily store values with single-ampersand (&) and double-ampersand (&&) substitution. You can use the double-ampersand (&&) substitution variable if you want to reuse the variable 
value without prompting the user each time. The user sees the prompt for the value only once.

You can also predefine variables by using the DEFINE command. DEFINE creates and assigns a value to a variable. Use the UNDEFINE command to remove a variable.

DEFINE employee_num = 200

SELECT employee_id, last_name, salary, department_id
FROM employees
WHERE employee_id = &employee_num ;

UNDEFINE employee_num

Use substitution variables to supplement the following:

WHERE conditions

ORDER BY clauses

Column expressions

Table names

Entire SELECT statements

SELECT employee_id, last_name, salary, department_id
FROM employees
WHERE employee_id = &employee_num;

SELECT employee_id, last_name, job_id, &&column_name
FROM employees
ORDER BY &column_name ;



3) Text Fields vs. Numeric Fields

SQL requires single quotes around text values (most database systems will also allow double quotes). However, numeric fields should not be enclosed in quotes.


4) Operators in the WHERE Clause

The following operators can be used in the WHERE clause:

=     Equal

<>    Not equal. Note: In some versions of SQL this operator may be written as !=

>
Greater than

<     Less than

>=    Greater than or equal

<=    Less than or equal

BETWEEN...AND   To display rows based on a range of values

LIKE    Search for a pattern

IN    To specify multiple possible values for a column

IS NULL   Is a NULL value.

SELECT last_name, salary
FROM employees
WHERE salary <= 3000;

SELECT last_name, salary
FROM employees
WHERE salary BETWEEN 2500 AND 3500;

SELECT last_name
FROM employees
WHERE last_name BETWEEN 'King' AND 'Smith';

SELECT employee_id, last_name, salary, manager_id
FROM employees
WHERE manager_id IN (100, 101, 201);

SELECT first_name
FROM employees
WHERE first_name LIKE 'S%'; 

% denotes zero or many characters.

_ denotes one character.

ESCAPE Identifier

When you need to have an exact match for the actual % and _ characters, use the ESCAPE identifier.This option specifies what the escape character is. If you want to search for strings that contain SA_, you can use the following SQL statement:

SELECT employee_id, last_name, job_id
FROM employees 
WHERE job_id LIKE '%SA\_%' ESCAPE '\';

SELECT last_name, manager_id
FROM employees
WHERE manager_id IS NULL;


5) The SQL AND, OR and NOT Operators

The WHERE clause can be combined with AND, OR, and NOT operators. The AND and OR operators are used to filter records based on more than one condition:

The AND operator displays a record if all the conditions separated by AND is TRUE.

SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary >= 10000
AND job_id LIKE '%MAN%';

The OR operator displays a record if any of the conditions separated by OR is TRUE.

SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary >= 10000
OR job_id LIKE '%MAN%';

The NOT operator displays a record if the condition(s) is NOT TRUE.

SELECT last_name, job_id
FROM employees
WHERE job_id
NOT IN ('IT_PROG', 'ST_CLERK', 'SA_REP');


6) The SQL ORDER BY Keyword

The ORDER BY keyword is used to sort the result-set in ascending or descending order. The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;

SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;


7) The SQL INSERT INTO Statement

The INSERT INTO statement is used to insert new records in a table. It is possible to write the INSERT INTO statement in two ways. The first way specifies both the column names and the values to be inserted:

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query. However, make sure the order of the values is in the same order as the columns in the table. The INSERT INTO syntax would be as follows:

INSERT INTO table_name
VALUES (value1, value2, value3, ...);

Inserting Special Values: The SYSDATE function records the current date and time.

INSERT INTO employees (employee_id, first_name, last_name,email, phone_number, hire_date, job_id, salary, commission_pct, manager_id, department_id)
VALUES (113, 'Louis', 'Popp','LPOPP', '515.124.4567',SYSDATE, 'AC_ACCOUNT', 6900,NULL, 205, 110);


8) Creating a Script

Use & substitution in a SQL statement to prompt for values.

INSERT INTO departments
(department_id, department_name, location_id)
VALUES (&department_id, '&department_name',&location);


9) Copying Rows from another Table

Do not use the VALUES clause. Match the number of columns in the INSERT clause to those in the subquery. Inserts all the rows returned by the subquery in the table, sales_reps.

INSERT INTO sales_reps(id, name, salary, commission_pct)
SELECT employee_id, last_name, salary, commission_pct
FROM employees
WHERE job_id LIKE '%REP%';


10) What is a NULL Value?

A field with a NULL value is a field with no value. If any column value in an arithmetic expression is null, the result is null. For example, if you attempt to perform division by zero, you 
get an error. However, if you divide a number by null, the result is a null or unknown.

If a field in a table is optional, it is possible to insert a new record or update a record without adding a value to this field. Then, the field will be saved with a NULL value.

Implicit method: Omit the column from the column list.

INSERT INTO departments (department_id,department_name) VALUES (30, 'Purchasing');

Explicit method: Specify the NULL keyword in the VALUES clause.

INSERT INTO departments VALUES (100, 'Finance', NULL, NULL);


11) How to Test for NULL Values?

It is not possible to test for NULL values with comparison operators, such as =, <, or <>. We will have to use the IS NULL and IS NOT NULL operators instead.

IS NULL Syntax

SELECT column_names
FROM table_name
WHERE column_name IS NULL;

IS NOT NULL Syntax

SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;


12) The SQL SELECT TOP Clause

The SELECT TOP clause is used to specify the number of records to return. The SELECT TOP clause is useful on large tables with thousands of records. Returning a large number of records can impact on performance.

SQL Server / MS Access Syntax:

SELECT TOP number|percent column_name(s)
FROM table_name
WHERE condition;

Oracle Syntax:

SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number;
SELECT TOP 50 PERCENT * FROM Customers;


