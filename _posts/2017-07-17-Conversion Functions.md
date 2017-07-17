---
layout: post
title: SQL - Conversion-Functions
---

{{ page.title }}
================

1) Implicit data type conversion

Oracle server can automatically perform data type conversion in an expression. For example, the expression hire_date > '01-JAN-90' results in the implicit conversion from the string '01-JAN-90' to a date. Therefore, a VARCHAR2 or CHAR value can be implicitly converted to a number or date data type in an expression.

In general, the Oracle server uses the rule for expressions when a data type conversion is needed. For example, the expression grade = 2 results in the implicit conversion of the number 20000 to the string “2” because grade is a CHAR(2) column.

2) Explicit data type conversion

Explicit data type conversions are done by using the conversion functions. Conversion functions convert a value from one data type to another. Generally, the form of the function names follows the convention data type TO data type.The first data type is the input data type and the second data type is the output.

2.1) TO_CHAR(number|date,[ fmt],[nlsparams]) : Converts a number or date value to a VARCHAR2 character string with the format model fmt

SELECT employee_id, TO_CHAR(hire_date, 'MM/YY') Month_Hired
FROM employees
WHERE last_name = 'Higgins';

SELECT TO_CHAR(salary, '$99,999.00') SALARY
FROM employees
WHERE last_name = 'Ernst';

SELECT TO_CHAR(NEXT_DAY(ADD_MONTHS(hire_date, 6), 'FRIDAY'),'fmDay, Month ddth, YYYY') "Next 6 Month Review"
FROM employees
ORDER BY hire_date;

2.2) TO_NUMBER(char,[fmt],[nlsparams])  : Converts a character string containing digits to a number in the format specified by the optional format model fmt.

SELECT TO_NUMBER('5467.12') FROM DUAL;

SELECT TO_NUMBER('5467.12', '999999.99') FROM DUAL;

2.3) TO_DATE(char,[fmt],[nlsparaMS]) : Converts a character string representing a date to a date value according to the fmt that is specified. If fmt is omitted, the format is DD-MON-YY.

SELECT last_name, hire_date
FROM employees
WHERE hire_date = TO_DATE('May 24, 1999', 'fxMonth DD, YYYY');

SELECT last_name, TO_CHAR(hire_date, 'DD-Mon-YYYY')
FROM employees
WHERE hire_date < TO_DATE('01-Jan-90','DD-Mon-RR');

3) Nesting Functions

The following SQL example displays the last names of employees in department 60. The evaluation of the SQL statement involves three steps:

SELECT last_name,UPPER(CONCAT(SUBSTR (LAST_NAME, 1, 8), '_US'))
FROM employees
WHERE department_id = 60;

a. The inner function retrieves the first eight characters of the last name.

Result1 = SUBSTR (LAST_NAME, 1, 8)

b. The outer function concatenates the result with _US.

Result2 = CONCAT(Result1, '_US')

c. The outermost function converts the results to uppercase.

The entire expression becomes the column heading because no column alias was given.

4) General Functions

These functions work with any data type and pertain to the use of null values in the expression list.

a. NVL :- Converts a null value to an actual value.

SELECT last_name, salary, NVL(commission_pct, 0),(salary*12) + (salary*12*NVL(commission_pct, 0)) AN_SAL
FROM employees;


b. NVL2 :- If expr1 is not null, NVL2 returns expr2. If expr1 is null, NVL2 returns expr3. The argument expr1 can have any data type.

SELECT last_name, salary, commission_pct,NVL2(commission_pct,'SAL+COMM', 'SAL') income
FROM employees 
WHERE department_id IN (50, 80);

c. NULLIF :- Compares two expressions and returns null if they are equal; returns the first expression if they are not equal.

SELECT first_name, LENGTH(first_name) "expr1",last_name, LENGTH(last_name) "expr2",NULLIF(LENGTH(first_name), LENGTH(last_name)) result
FROM employees;

d. COALESCE Returns the first non-null expression in the expression list.

SELECT last_name, employee_id,COALESCE(TO_CHAR(commission_pct),TO_CHAR(manager_id),
'No commission and no manager')
FROM employees;

5)	CASE and DECODE

Provide the use of the IF-THEN-ELSE logic within a SQL statement.

•	CASE expression

SELECT last_name, job_id, salary,
CASE job_id WHEN 'IT_PROG' THEN 1.10*salary
WHEN 'ST_CLERK' THEN 1.15*salary
WHEN 'SA_REP' THEN 1.20*salary
ELSE salary END "REVISED_SALARY"
FROM employees;

•	DECODE function

SELECT last_name, job_id, salary,
DECODE(job_id, 'IT_PROG', 1.10*salary,
'ST_CLERK', 1.15*salary,
'SA_REP', 1.20*salary,
salary) REVISED_SALARY
FROM employees;

The CASE expression complies with the ANSI SQL. The DECODE function is specific to Oracle syntax.
