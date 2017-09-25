---
layout: post
title: SQL - Manipulating Data
---

{{ page.title }}
================


1) Data Manipulation Language

• A DML statement is executed when you:

– Add new rows to a table

– Modify existing rows in a table

– Remove existing rows from a table

• A transaction consists of a collection of DML statements that form a logical unit of work.

2) Adding a New Row to a Table

• Add new rows to a table by using the INSERT statement.

INSERT INTO departments(department_id,department_name, manager_id, location_id) VALUES (70, 'Public Relations', 100, 1700);

• Enclose character and date values within single quotation marks.

3) Inserting Rows with Null Values

• Implicit method: Omit the column from the column list.

INSERT INTO departments (department_id,department_name) VALUES (30, 'Purchasing');

• Explicit method: Specify the NULL keyword in the VALUES clause

INSERT INTO departments VALUES (100, 'Finance', NULL, NULL);

4) Inserting Special Values

• The SYSDATE function records the current date and time.

INSERT INTO employees (employee_id,first_name, last_name,email, phone_number,hire_date, job_id, salary,commission_pct, manager_id,department_id) VALUES (113,'Louis', 'Popp','LPOPP','515.124.4567',SYSDATE, 'AC_ACCOUNT', 6900,NULL, 205, 110);

5) Inserting Specific Date and Time Values

• Add a new employee.

INSERT INTO employees VALUES (114,'Den', 'Raphealy','DRAPHEAL', '515.127.4561',TO_DATE('FEB 3, 1999', 'MON DD, YYYY'),'SA_REP', 11000, 0.2, 100, 60);

• If a date must be entered in a format other than the default format (for example, with another century or a specific time), you must use the TO_DATE function.

6) Creating a Script

• Use & substitution in a SQL statement to prompt for values.

• & is a placeholder for the variable value.

INSERT INTO departments(department_id, department_name, location_id) VALUES (&department_id, '&department_name',&location);

7) Copying Rows from Another Table

• Write your INSERT statement with a subquery

INSERT INTO sales_reps(id, name, salary, commission_pct) SELECT employee_id, last_name, salary, commission_pct FROM employees WHERE job_id LIKE '%REP%';

• Do not use the VALUES clause.

• Match the number of columns in the INSERT clause to those in the subquery.

8) Changing Data in a Table

• Modify existing values in a table with the UPDATE statement.

• Values for a specific row or rows are modified if you specify the WHERE clause:

UPDATE employees SET department_id = 50 WHERE employee_id = 113;

• Values for all the rows in the table are modified if you omit the WHERE clause:

UPDATE copy_emp SET department_id = 110;

9) Updating Two Columns with a Subquery

• Update employee 113’s job and salary to match those of employee 205.

UPDATE employees SET job_id = (SELECT job_id FROM employees WHERE employee_id = 205),salary = (SELECT salary FROM employees WHERE employee_id = 205) WHERE employee_id = 113;

10) Updating Rows Based on Another Table

• Use the subqueries in the UPDATE statements to update row values in a table based on values from another table.

UPDATE copy_emp SET department_id = (SELECT department_id FROM employees WHERE employee_id = 100) WHERE job_id = (SELECT job_id FROM employees WHERE employee_id = 200);

11) Removing a Row from a Table

• You can remove existing rows from a table by using the DELETE statement.

• Specific rows are deleted if you specify the WHERE clause:

DELETE FROM departments WHERE department_name = ‘Finance';

• All rows in the table are deleted if you omit the WHERE clause:

DELETE FROM copy_emp;

12) Deleting Rows Based on Another Table

• Use the subqueries in the DELETE statements to remove rows from a table based on values from another table.

DELETE FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE department_name LIKE '%Public%');

13) TRUNCATE Statement

• Removes all rows from a table, leaving the table empty and the table structure intact.

• Is a data definition language (DDL) statement rather than a DML statement; cannot easily be undone.

TRUNCATE TABLE copy_emp;

14) Database Transactions

A database transaction consists of one of the following:

• DML statements that constitute one consistent change to the data

• One DDL statement

• One data control language (DCL) statement


15) Advantages of COMMIT and ROLLBACK Statements

With COMMIT and ROLLBACK statements, you can:

• Ensure data consistency

• Preview data changes before making changes permanent

• Group logically-related operations

16) Rolling Back Changes to a Marker

• Create a marker in the current transaction by using the SAVEPOINT statement.

• Roll back to that marker by using the ROLLBACK TO SAVEPOINT statement.

UPDATE...
SAVEPOINT update_done;

INSERT...
ROLLBACK TO update_done;


17) State of the Data Before COMMIT or ROLLBACK

• The previous state of the data can be recovered.

• The current user can review the results of the DML operations by using the SELECT statement.

• Other users cannot view the results of the DML statements issued by the current user.

• The affected rows are locked; other users cannot change the data in the affected rows.

18) State of the Data After COMMIT

• Data changes are saved in the database.

• The previous state of the data is overwritten.

• All users can view the results.

• Locks on the affected rows are released; those rows are available for other users to manipulate.

• All savepoints are erased.

19) State of the Data After ROLLBACK

• Discard all pending changes by using the ROLLBACK statement:

• Data changes are undone.

• Previous state of the data is restored.

• Locks on the affected rows are released.

DELETE FROM copy_emp;

ROLLBACK ;

20) FOR UPDATE Clause in a SELECT Statement

• Locks the rows in the EMPLOYEES table where job_id is SA_REP.

SELECT employee_id, salary, commission_pct, job_id
FROM employees
WHERE job_id = 'SA_REP'
FOR UPDATE
ORDER BY employee_id;

• Lock is released only when you issue a ROLLBACK or a COMMIT.

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples

