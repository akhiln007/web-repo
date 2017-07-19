---
layout: post
title: SQL - Aggregated Data Using Group Functions
---

{{ page.title }}
================

1) What are Group functions:

Group functions operate on sets of rows to give one result per group.

 • AVG :- Average value of n, ignoring null values.

 • COUNT :- Number of rows.

 • MAX :- Maximum value of expr, ignoring null values.

 • MIN :- Minimum value of expr, ignoring null values.

 • STDDEV :- Standard deviation of n, ignoring null values.

 • SUM :- Sum values of n, ignoring null values.

 • VARIANCE :- Variance of n, ignoring null values


1.a) Guidelines for using the group functions:

• DISTINCT makes the function consider only nonduplicate values; ALL makes it consider every value, including duplicates. The default is ALL and therefore does not need to be specified.

• The data types for the functions with an expr argument may be CHAR, VARCHAR2, NUMBER, or DATE.

• All group functions ignore null values. To substitute a value for null values, use the NVL, NVL2, or COALESCE functions.


2) SQL MIN() and MAX() Functions

You can use the MAX and MIN functions for numeric, character and date data types. The MIN() function returns the smallest value of the selected column. The MAX() function returns the largest value of the selected column.

SELECT MIN(last_name), MAX(last_name) FROM employees;

3) SQL COUNT(), AVG() and SUM() Functions

3.a) The COUNT() function returns the number of rows that matches a specified criteria.

COUNT(*) returns the number of rows in a table:

SELECT COUNT(*)
FROM employees
WHERE department_id = 50;

COUNT(expr) returns the number of rows with non-null values for expr:

SELECT COUNT(commission_pct)
FROM employees
WHERE department_id = 80;

SELECT COUNT(DISTINCT department_id)
FROM employees;

3.b) The AVG() function returns the average value of a numeric column.

Group functions ignore null values in the column:

SELECT AVG(commission_pct) FROM employees;

The NVL function forces group functions to include null values:

SELECT AVG(NVL(commission_pct, 0)) FROM employees;


3.c) The SUM() function returns the total sum of a numeric column.

SELECT AVG(salary), MAX(salary),
MIN(salary), SUM(salary)
FROM employees
WHERE job_id LIKE '%REP%';


4) SQL LIKE Operator

The LIKE operator is used in a WHERE clause to search for a specified pattern in a column. There are two wildcards used in conjunction with the LIKE operator:

% - The percent sign represents zero, one, or multiple characters

_ - The underscore represents a single character

SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;

4.a) ESCAPE Identifier 

When you need to have an exact match for the actual % and _ characters, use the ESCAPE identifier. This option specifies what the escape character is. If you want to search for strings that 

contain SA_, you can use the following SQL statement:

SELECT employee_id, last_name, job_id
FROM employees WHERE job_id LIKE '%SA\_%' ESCAPE '\';

5) SQL IN Operator

The IN operator allows you to specify multiple values in a WHERE clause. The IN operator is a shorthand for multiple OR conditions.

SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);

SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);


6) SQL GROUP BY Statement

The GROUP BY statement is often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns. All columns in the SELECT list that are not in group functions must be in the GROUP BY clause. 

SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);

The GROUP BY column does not have to be in the SELECT list.

SELECT AVG(salary)
FROM employees
GROUP BY department_id ;


SELECT department_id dept_id, job_id, SUM(salary)
FROM employees
GROUP BY department_id, job_id
ORDER BY department_id;

7) SQL HAVING Clause

The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions.You cannot use the WHERE clause to restrict groups. You use the HAVING clause to restrict groups. You cannot use group functions in the WHERE clause.

SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;

SELECT department_id, MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary)>10000;

SELECT job_id, SUM(salary) PAYROLL
FROM employees
WHERE job_id NOT LIKE '%REP%'
GROUP BY job_id
HAVING SUM(salary) > 13000
ORDER BY SUM(salary);

8) Nesting Group Functions

Group functions can be nested to a depth of two functions.

SELECT MAX(AVG(salary))
FROM employees
GROUP BY department_id;
