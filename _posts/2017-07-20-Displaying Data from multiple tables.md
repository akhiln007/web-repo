---
layout: post
title: SQL - Displaying Data from multiple tables
---

{{ page.title }}
================

1) SQL Joins

A JOIN clause is used to combine rows from two or more tables, based on a related column between them. Joins that are compliant with the SQL:1999 standard.


2) Ambiguous Column Names

Use table prefixes to qualify column names that are in multiple tables.

• Use table prefixes to improve performance.

• Instead of full table name prefixes, use table aliases.

• Table alias gives a table a shorter name:


2) Natural joins:

– NATURAL JOIN clause

• The NATURAL JOIN clause is based on all columns in the two tables that have the same name.

• It selects rows from the two tables that have equal values in all matched columns.

• If the columns having the same names have different data types, an error is returned.


SELECT department_id, department_name,
location_id, city
FROM departments
NATURAL JOIN locations;

3) USING clause

• If several columns have the same names but the data types do not match, natural join can be applied using the USING clause to specify the columns that should be used for an equijoin.

• Use the USING clause to match only one column when more than one column matches.

• The NATURAL JOIN and USING clauses are mutually exclusive.


SELECT employee_id, last_name,
location_id, department_id
FROM employees JOIN departments
USING (department_id) ;

4) ON clause

• The join condition for the natural join is basically an equijoin of all columns with the same name.

• Use the ON clause to specify arbitrary conditions or specify columns to join.

• The join condition is separated from other search conditions.

• The ON clause makes code easy to understand.

SELECT e.employee_id, e.last_name, e.department_id,
d.department_id, d.location_id
FROM employees e JOIN departments d
ON (e.department_id = d.department_id);

SELECT employee_id, city, department_name
FROM employees e
JOIN departments d
ON d.department_id = e.department_id
JOIN locations l
ON d.location_id = l.location_id;

• Use the AND clause or the WHERE clause to apply additional conditions:

SELECT e.employee_id, e.last_name, e.department_id,
d.department_id, d.location_id
FROM employees e JOIN departments d
ON (e.department_id = d.department_id)
AND e.manager_id = 149 ;

SELECT e.employee_id, e.last_name, e.department_id,
d.department_id, d.location_id
FROM employees e JOIN departments d
ON (e.department_id = d.department_id)
WHERE e.manager_id = 149 ;



5) SELF Join

Sometimes you need to join a table to itself. To find the name of each employee’s manager, you need to join the EMPLOYEES table to itself, or perform a self-join.

SELECT worker.last_name emp, manager.last_name mgr
FROM employees worker JOIN employees manager
ON (worker.manager_id = manager.employee_id);


6) Non equijoins

A nonequijoin is a join condition containing something other than an equality operator.

SELECT e.last_name, e.salary, j.grade_level
FROM employees e JOIN job_grades j
ON e.salary
BETWEEN j.lowest_sal AND j.highest_sal;

7) SQL INNER JOIN Keyword

The INNER JOIN keyword selects records that have matching values in both tables. Joining tables with the NATURAL JOIN, USING, or ON clauses results in an inner join. Any unmatched rows are not displayed in the output. To return the unmatched rows, you can use an outer join.

(INNER) JOIN: Returns records that have matching values in both tables

SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;

SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);

8) SQL LEFT JOIN Keyword

The LEFT JOIN keyword returns all records from the left table (table1), and the matched records from the right table (table2). The result is NULL from the right side, if there is no match.

This query retrieves all rows in the EMPLOYEES table, which is the left table, even if there is no match in the DEPARTMENTS table.

SELECT e.last_name, e.department_id, d.department_name
FROM employees e LEFT OUTER JOIN departments d
ON (e.department_id = d.department_id) ;

9) SQL RIGHT JOIN Keyword

The RIGHT JOIN keyword returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side, when there is no match.

The following query retrieves all rows in the DEPARTMENTS table, which is the right table, even if there is no match in the EMPLOYEES table.

SELECT e.last_name, e.department_id, d.department_name
FROM employees e RIGHT OUTER JOIN departments d
ON (e.department_id = d.department_id) ;


10) SQL FULL OUTER JOIN Keyword

The FULL OUTER JOIN keyword return all records when there is a match in either left (table1) or right (table2) table records.Note: FULL OUTER JOIN can potentially return very large result-sets!

The following query retrieves all rows in the EMPLOYEES table, even if there is no match in the DEPARTMENTS table. It also retrieves all rows in the DEPARTMENTS table, even if there is no match in the EMPLOYEES table.

SELECT e.last_name, d.department_id, d.department_name
FROM employees e FULL OUTER JOIN departments d
ON (e.department_id = d.department_id) ;

11) Cartesian Products

A Cartesian product is formed when:

–	A join condition is omitted

–	A join condition is invalid

–	All rows in the first table are joined to all rows in the second table

• To avoid a Cartesian product, always include a valid join condition.

The CROSS JOIN clause produces the cross-product of two tables.

• This is also called a Cartesian product between the two tables.

SELECT last_name, department_name
FROM employees
CROSS JOIN departments;





