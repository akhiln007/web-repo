---
layout: post
title: SQL - Subqueries
---

{{ page.title }}
================


1) Subqueries

You can write subqueries in the WHERE clause of another SQL statement to obtain values based on an unknown conditional value.

SELECT select_list
FROM table
WHERE expr operator
(SELECT select_list
FROM table);

You can place the subquery in a number of SQL clauses, including the following:

• WHERE clause

• HAVING clause

• FROM clause

Using a Subquery to Solve a Problem:- Who has a salary greater than Abel’s?

Main query: Which employees have salaries greater than Abel’s salary?

Subquery  : What is Abel’s salary?

SELECT last_name, salary
FROM employees
WHERE salary >
(SELECT salary
FROM employees
WHERE last_name = 'Abel');

2) Guidelines for Using Subqueries

• Enclose subqueries in parentheses.

• Place subqueries on the right side of the comparison condition for readability (However, the subquery can appear on either side of the comparison operator.).

• Use single-row operators with single-row subqueries and multiple-row operators with multiple-row subqueries.

3) Types of Subqueries

Single-row subqueries: Queries that return only one row from the inner SELECT statement.

single-row operators (>, =, >=, <, <>, <=).

Multiple-row subqueries: Queries that return more than one row from the inner SELECT statement.

multiple-row operators (IN, ANY, ALL).

4) Single-Row Subqueries

A single-row subquery is one that returns one row from the inner SELECT statement. This type of subquery uses a single-row operator.

Display the employees whose job ID is the same as that of employee 141:

SELECT last_name, job_id
FROM employees
WHERE job_id =(SELECT job_id FROM employees WHERE employee_id = 141);

• Using Group Functions in a Subquery

SELECT last_name, job_id, salary
FROM employees
WHERE salary =(SELECT MIN(salary) FROM employees);

• The HAVING Clause with Subqueries

SELECT department_id, MIN(salary)
FROM employees
GROUP BY department_id
HAVING MIN(salary) > (SELECT MIN(salary) FROM employees WHERE department_id = 50);

5) Multiple-Row Subqueries

Subqueries that return more than one row are called multiple-row subqueries. You use a multiple-row operator, instead of a single-row operator, with a multiple-row subquery. The multiple-row operator expects one or more values.

• IN Equal to any member in the list

SELECT last_name, salary, department_id
FROM employees
WHERE salary IN (SELECT MIN(salary) FROM employees GROUP BY department_id);

• ANY Must be preceded by =, !=, >, <, <=, >= Compares a value to each value in a list or returned by a query. Evaluates to FALSE if the query returns no rows.

SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ANY (SELECT salary FROM employees WHERE job_id = 'IT_PROG') AND job_id <>  'IT_PROG';

The ANY operator (and its synonym, the SOME operator) compares a value to each value returned by a subquery. The example displays employees who are not IT programmers and whose salary is less than that of any IT programmer. The maximum salary that a programmer earns is $9,000. < ANY means less than the maximum. >ANY means more than the minimum. =ANY is equivalent to
IN.

• ALL Must be preceded by =, !=, >, <, <=, >=. Compares a value to every value in a list or returned by a query. Evaluates to TRUE if the query returns no rows.

SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ALL
(SELECT salary 
FROM employees
WHERE job_id = 'IT_PROG')
AND job_id <> 'IT_PROG';

The ALL operator compares a value to every value returned by a subquery. The example displays employees whose salary is less than the salary of all employees with a job ID of IT_PROG
and whose job is not IT_PROG. >ALL means more than the maximum and <ALL means less than the minimum. The NOT operator can be used with IN, ANY, and ALL operators.

6) Null Values in a Subquery

The example SQL statement attempts to display all the employees who do not have any subordinates. Logically, this SQL statement should have returned 12 rows. However, the SQL statement does not return any rows. One of the values returned by the inner query is a null value, and, therefore, the entire query returns no rows. The reason is that all conditions that compare a null value result in a null. So whenever null values are likely to be part of the results set of a subquery, do not use the NOT IN operator. The NOT IN operator is equivalent to <> ALL.

SELECT emp.last_name
FROM employees emp
WHERE emp.employee_id NOT IN (SELECT mgr.manager_id FROM employees mgr);


References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
