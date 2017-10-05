---
layout: post
title: SQL - Manipulating Large Data Sets
---

{{ page.title }}
================


1) Using Subqueries to Manipulate Data

You can use subqueries in data manipulation language (DML) statements to:

• Retrieve data using an inline view

• Copy data from one table to another

• Update data in one table based on the values of another table

• Delete rows from one table based on rows in another table

2) Retrieving Data Using a Subquery as Source

SELECT department_name, city FROM departments NATURAL JOIN (SELECT l.location_id, l.city, l.country_id FROM loc l JOIN countries c ON(l.country_id = c.country_id) JOIN regions USING (region_id) WHERE region_name = 'Europe');

3) Inserting Using a Subquery as a Target

INSERT INTO (SELECT l.location_id, l.city, l.country_id FROM loc l JOIN countries c ON(l.country_id = c.country_id) JOIN regions USING(region_id) WHERE region_name = 'Europe') VALUES (3300, 'Cardiff', 'UK');

4) Using the WITH CHECK OPTION Keyword on DML Statements

The WITH CHECK OPTION keyword prohibits you from changing rows that are not in the subquery.

INSERT INTO (SELECT location_id, city, country_id FROM loc WHERE country_id IN (SELECT country_id FROM countries NATURAL JOIN regions WHERE region_name = 'Europe') WITH CHECK OPTION ) VALUES (3600, 'Washington', 'US');

5) Overview of the Explicit Default Feature

• Use the DEFAULT keyword as a column value where the default column value is desired.

• This allows the user to control where and when the default value should be applied to data.

• Explicit defaults can be used in INSERT and UPDATE statements.


6) Using Explicit Default Values

• DEFAULT with INSERT:

INSERT INTO deptm3 (department_id, department_name, manager_id) VALUES (300, 'Engineering', DEFAULT);

• DEFAULT with UPDATE:

UPDATE deptm3 SET manager_id = DEFAULT WHERE department_id = 10;

7) Copying Rows from Another Table

• Write your INSERT statement with a subquery.

INSERT INTO sales_reps(id, name, salary, commission_pct) SELECT employee_id, last_name, salary, commission_pct FROM employees WHERE job_id LIKE '%REP%';

• Do not use the VALUES clause.

• Match the number of columns in the INSERT clause with that in the subquery.

8) Overview of Multitable INSERT Statements

• Use the INSERT…SELECT statement to insert rows into multiple tables as part of a single DML statement.

• They provide significant performance improvement over:

 - Single DML versus multiple INSERT....SELECT statements.

 - Single DML versus a procedure to perform multiple inserts by using the IF...THEN syntax

9) Types of Multitable INSERT Statements

The different types of multitable INSERT statements are:

• Unconditional INSERT

For each row returned by the subquery, a row is inserted into each of the target tables.

INSERT ALL INTO sal_history VALUES(EMPID,HIREDATE,SAL) INTO mgr_history VALUES(EMPID,MGR,SAL) SELECT employee_id EMPID, hire_date HIREDATE,salary SAL, manager_id MGR FROM employees WHERE employee_id > 200;

• Conditional INSERT ALL

For each row returned by the subquery, a row is inserted into each target table if the specified condition is met.

INSERT ALL WHEN HIREDATE < '01-JAN-95' THEN INTO emp_history VALUES(EMPID,HIREDATE,SAL)  WHEN COMM IS NOT NULL THEN INTO emp_sales VALUES(EMPID,COMM,SAL) SELECT employee_id EMPID, hire_date HIREDATE,salary SAL, commission_pct COMM FROM employees

• Pivoting INSERT

This is a special case of the unconditional INSERT ALL.

INSERT ALL INTO sales_info VALUES (employee_id,week_id,sales_MON) INTO sales_info VALUES (employee_id,week_id,sales_TUE) INTO sales_info VALUES (employee_id,week_id,sales_WED) INTO sales_info VALUES (employee_id,week_id,sales_THUR) INTO sales_info VALUES (employee_id,week_id, sales_FRI) SELECT EMPLOYEE_ID, week_id, sales_MON, sales_TUE,sales_WED, sales_THUR,sales_FRI FROM sales_source_data;

• Conditional INSERT FIRST

For each row returned by the subquery, a row is inserted into the very first target table in which the condition is met.

INSERT FIRST WHEN salary < 5000 THEN INTO sal_low VALUES (employee_id, last_name, salary) WHEN salary between 5000 and 10000 THEN INTO sal_mid VALUES (employee_id, last_name, salary) ELSE INTO sal_high VALUES (employee_id, last_name, salary) SELECT employee_id, last_name, salary FROM employees

10) MERGE Statement

• Provides the ability to conditionally update, insert, or delete data into a database table

• Performs an UPDATE if the row exists, and an INSERT if it is a new row:

– Avoids separate updates

– Increases performance and ease of use

– Is useful in data warehousing applications

MERGE INTO copy_emp3 c USING (SELECT * FROM EMPLOYEES ) e ON (c.employee_id = e.employee_id) WHEN MATCHED THEN UPDATE SET c.first_name = e.first_name, c.last_name = e.last_name,
...
DELETE WHERE (E.COMMISSION_PCT IS NOT NULL) WHEN NOT MATCHED THEN INSERT VALUES(e.employee_id, e.first_name,

11) Tracking Changes in Data

SELECT salary FROM employees3 WHERE employee_id = 107;

UPDATE employees3 SET salary = salary * 1.30 WHERE employee_id = 107;

commit;

SELECT salary FROM employees3 VERSIONS BETWEEN SCN MINVALUE AND MAXVALUE WHERE employee_id = 107;

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
