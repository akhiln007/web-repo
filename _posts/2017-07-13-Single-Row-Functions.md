---
layout: post
title: SQL - Single Row Functions
---

{{ page.title }}
================

1) SQL Functions

Functions are a very powerful feature of SQL. They can be used to do the following:

• Perform calculations on data

• Modify individual data items

• Manipulate output for groups of rows

• Format dates and numbers for display

• Convert column data types


2) Two Types of SQL Functions

There are two types of functions:

Single-row functions and Multiple-row functions

Single-Row Functions

These functions operate on single rows only and return one result per row. There are different types of single-row functions. This lesson covers the following ones:

• Character

• Number

• Date

• Conversion

• General

Features of single-row functions include:

• Acting on each row that is returned in the query

• Returning one result per row

• Possibly returning a data value of a different type than the one that is referenced

• Possibly expecting one or more arguments

• Can be used in SELECT, WHERE, and ORDER BY clauses; can be nested


The following single-row functions are discussed in the next lesson titled “Using Conversion Functions"

• Conversion functions: Convert a value from one data type to another

• General functions:

- NVL

- NVL2

- NULLIF

- COALESCE

- CASE

- DECODE

Multiple-Row Functions

Functions can manipulate groups of rows to give one result per group of rows. These functions are also known as group functions.


3) Character Functions

Single-row character functions accept character data as input and can return both character and numeric values. Character functions can be divided into the following:

• Case-conversion functions

LOWER

UPPER

INITCAP

SELECT 'The job id for '||UPPER(last_name)||' is '
||LOWER(job_id) AS "EMPLOYEE DETAILS"
FROM employees;


• Character-manipulation functions

CONCAT('Hello', 'World') 

HelloWorld

TRIM('H' FROM 'HelloWorld') 

elloWorld

SUBSTR('HelloWorld',1,5) 

Hello

LENGTH('HelloWorld') 

10

INSTR('HelloWorld', 'W') 

6

LPAD(salary,10,'*') 

*****24000

RPAD(salary, 10, '*') 

24000*****

REPLACE('JACK and JUE','J','BL')

BLACK and BLUE


4) Number Functions

ROUND(45.926, 2) 

45.93

TRUNC(45.926, 2) 

45.92

MOD(1600, 300) 

100


5) Working with Dates

The Oracle database stores dates in an internal numeric format: century, year, month, day, hours, minutes, and seconds.

• The default date display format is DD-MON-RR.

– Enables you to store 21st-century dates in the 20th century by specifying only the last two digits of the year 

– Enables you to store 20th-century dates in the 21st century in the same way

RR Date Format

The RR date format is similar to the YY element, but you can use it to specify different centuries. Use the RR date format element instead of YY so that the century of the return value varies according to the specified two-digit year and the last two digits of the current year.

Current Year Given Date Interpreted (RR) Interpreted (YY)

1994 -> 27-OCT-95 -> 1995 -> 1995

1994 -> 27-OCT-17 -> 2017 -> 1917

2001 -> 27-OCT-17 -> 2017 -> 2017


6) SYSDATE Function

SYSDATE is a function that returns:

• Date

• Time


7) Arithmetic with Dates

• Add or subtract a number to or from a date for a resultant date value.

• Subtract two dates to find the number of days between those dates.

• Add hours to a date by dividing the number of hours by 24.


date + number = Date (Adds a number of days to a date)

date – number = Date (Subtracts a number of days from a date)

date – date   = Number of days (Subtracts one date from another)

date + number/24 = Date (Adds a number of hours to a date)

SELECT last_name, (SYSDATE-hire_date)/7 AS WEEKS
FROM employees
WHERE department_id = 90;


8) Date-Manipulation Functions

• MONTHS_BETWEEN('01-SEP-95','11-JAN-94')	

19.6774194

• ADD_MONTHS (‘31-JAN-96',1)

‘29-FEB-96'

• NEXT_DAY ('01-SEP-95','FRIDAY')

'08-SEP-95'

• LAST_DAY ('01-FEB-95')

'28-FEB-95'


9) Using ROUND and TRUNC Functions with Dates

Assume SYSDATE = '25-JUL-03':

• ROUND(SYSDATE,'MONTH') 

01-AUG-03

• ROUND(SYSDATE ,'YEAR') 

01-JAN-04

• TRUNC(SYSDATE ,'MONTH') 

01-JUL-03

• TRUNC(SYSDATE ,'YEAR') 

01-JAN-03
