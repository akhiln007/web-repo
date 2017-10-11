---
layout: post
title: SQL - Retrieving Data Using Subqueries
---

{{ page.title }}
================

1) Multiple-Column Subqueries

Multiple-column comparisons involving subqueries can be:

• Pairwise comparisons

Display the details of the employees who are managed by the same manager and work in the same department as employees with the first name of “John.”

SELECT employee_id, manager_id, department_id FROM empl_demo WHERE (manager_id, department_id) IN(SELECT manager_id, department_id FROM empl_demo WHERE first_name = 'John') AND first_name<> 'John';


• Nonpairwise comparisons

Display the details of the employees who are managed by the same manager as the employees with the first name of “John” and work in the same department as the employees with the first name of “John.”

SELECT employee_id, manager_id, department_id FROM empl_demo WHERE manager_id IN (SELECT manager_id FROM empl_demo WHERE first_name = 'John') AND department_id IN (SELECT department_id
FROM empl_demo WHERE first_name = 'John') AND first_name <> 'John';

2) Scalar Subquery Expressions

• A scalar subquery expression is a subquery that returns exactly one column value from one row.

• Scalar subqueries can be used in:

– The condition and expression part of DECODE and CASE

– All clauses of SELECT except GROUP BY

– The SET clause and WHERE clause of an UPDATE statement

3) Scalar Subqueries: Examples

• Scalar subqueries in CASE expressions:

SELECT employee_id, last_name,(CASE WHEN department_id =(SELECT department_id FROM departments WHERE location_id = 1800) THEN 'Canada' ELSE 'USA' END) location FROM employees;

• Scalar subqueries in the ORDER BY clause:

SELECT employee_id, last_name FROM employees e ORDER BY (SELECT department_name FROM departments d WHERE e.department_id = d.department_id);

4) Correlated Subqueries

Correlated subqueries are used for row-by-row processing. Each subquery is executed once for every row of the outer query.

Nested Subquery Execution

• The inner query executes first and finds a value.

• The outer query executes once, using the value from the inner query.

Correlated Subquery Execution

• Get a candidate row (fetched by the outer query).

• Execute the inner query using the value of the candidate row.

• Use the values resulting from the inner query to qualify or disqualify the candidate.

• Repeat until no candidate row remains.

5) Using Correlated Subqueries

• Find all employees who earn more than the average salary in their department.

SELECT last_name, salary, department_id FROM employees outer WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = outer.department_id);

Each time a row from the outer query is processed, the inner query is evaluated.

• Display details of those employees who have changed jobs at least twice.

SELECT e.employee_id, last_name,e.job_id FROM employees e WHERE 2 <= (SELECT COUNT(*) FROM job_history WHERE employee_id = e.employee_id);

6) Using the EXISTS Operator

• The EXISTS operator tests for existence of rows in the results set of the subquery.

• If a subquery row value is found:

– The search does not continue in the inner query

– The condition is flagged TRUE

• If a subquery row value is not found:

– The condition is flagged FALSE

– The search continues in the inner query

SELECT employee_id, last_name, job_id, department_id FROM employees outer WHERE EXISTS ( SELECT 'X' FROM employees WHERE manager_id = outer.employee_id);

7) Using the NOT EXISTS Operator

• Find All Departments That Do Not Have Any Employees

SELECT department_id, department_name FROM departments d WHERE NOT EXISTS (SELECT 'X' FROM employees WHERE department_id = d.department_id);

• Alternative Solution

A NOT IN construct can be used as an alternative for a NOT EXISTS operator, as shown in the following example

SELECT department_id, department_name FROM departments WHERE department_id NOT IN (SELECT department_id FROM employees);

8) Using Correlated UPDATE

• Denormalize the EMPL6 table by adding a column to store the department name.

• Populate the table by using a correlated update.

ALTER TABLE empl6 ADD(department_name VARCHAR2(25));

UPDATE empl6 e SET department_name = (SELECT department_name FROM departments d WHERE e.department_id = d.department_id);

9) Correlated DELETE

Use a correlated subquery to delete rows in one table based on rows from another table. Use a correlated subquery to delete only those rows from the EMPL6 table that also exist in the EMP_HISTORY table.

DELETE FROM empl6 E WHERE employee_id = (SELECT employee_id FROM emp_history WHERE employee_id = E.employee_id);

10) Using the WITH clause

• Using the WITH clause, you can use the same query block in a SELECT statement when it occurs more than once within a complex query.

• The WITH clause retrieves the results of a query block and stores it in the user’s temporary tablespace.

• The WITH clause may improve performance.

• Using the WITH clause, write a query to display the department name and total salaries for those departments whose total salary is greater than the average salary across departments.

WITH dept_costs AS (SELECT d.department_name, SUM(e.salary) AS dept_total FROM employees e JOIN departments d ON e.department_id = d.department_id GROUP BY d.department_name),avg_cost AS (
SELECT SUM(dept_total)/COUNT(*) AS dept_avg FROM dept_costs) SELECT * FROM dept_costs WHERE dept_total > (SELECT dept_avg FROM avg_cost) ORDER BY department_name;

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
