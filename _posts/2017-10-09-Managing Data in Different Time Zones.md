---
layout: post
title: SQL - Managing Data in Different Time Zones
---

{{ page.title }}
================

1) TIME_ZONE Session Parameter

TIME_ZONE may be set to:

• An absolute offset

• Database time zone

• OS local time zone

• A named region

ALTER SESSION SET TIME_ZONE='-05:00';

ALTER SESSION SET TIME_ZONE=dbtimezone;

ALTER SESSION SET TIME_ZONE=local;

ALTER SESSION SET TIME_ZONE='America/New_York';

2) CURRENT_DATE, CURRENT_TIMESTAMP, and LOCALTIMESTAMP

• CURRENT_DATE:

– Returns the current date from the user session

– Has a data type of DATE

• CURRENT_TIMESTAMP:

– Returns the current date and time from the user session

– Has a data type of TIMESTAMP WITH TIME ZONE

• LOCALTIMESTAMP:

– Returns the current date and time from the user session

– Has a data type of TIMESTAMP

3) Comparing Date and Time in a Session’s Time Zone

The TIME_ZONE parameter is set to –5:00 and then SELECT statements for each date and time is executed to compare differences.

ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH24:MI:SS';

ALTER SESSION SET TIME_ZONE = '-5:00';

SELECT SESSIONTIMEZONE, CURRENT_DATE FROM DUAL;

SELECT SESSIONTIMEZONE, CURRENT_TIMESTAMP FROM DUAL;

SELECT SESSIONTIMEZONE, LOCALTIMESTAMP FROM DUAL;

4) DBTIMEZONE and SESSIONTIMEZONE

• Display the value of the database time zone:

SELECT DBTIMEZONE FROM DUAL;

• Display the value of the session’s time zone:

SELECT SESSIONTIMEZONE FROM DUAL;

5) TIMESTAMP Data Types

TIMESTAMP:- Year, Month, Day, Hour, Minute, Second with fractional seconds.

TIMESTAMP WITH TIME ZONE:- Same as the TIMESTAMP data type; also includes: TIMEZONE_HOUR, and TIMEZONE_MINUTE or TIMEZONE_REGION.

TIMESTAMP WITH LOCAL TIME ZONE:- Same as the TIMESTAMP data type; also includes a time zone offset in its value.

6) INTERVAL Data Types

• INTERVAL data types are used to store the difference between two datetime values.

• There are two classes of intervals:

– Year-month

– Day-time

• The precision of the interval is:

– The actual subset of fields that constitutes an interval

– Specified in the interval qualifier

7) EXTRACT

• Display the YEAR component from the SYSDATE.

SELECT EXTRACT (YEAR FROM SYSDATE) FROM DUAL;

• Display the MONTH component from the HIRE_DATE for those employees whose MANAGER_ID is 100.

SELECT last_name, hire_date,EXTRACT (MONTH FROM HIRE_DATE) FROM employees WHERE manager_id = 100;

SELECT EXTRACT ([YEAR] [MONTH][DAY] [HOUR] [MINUTE][SECOND] [TIMEZONE_HOUR] [TIMEZONE_MINUTE] [TIMEZONE_REGION] [TIMEZONE_ABBR] FROM [datetime_value_expression] [interval_value_expression]);

8) TZ_OFFSET

• Display the time zone offset for the 'US/Eastern', 'Canada/Yukon' and 'Europe/London' time zones:

SELECT TZ_OFFSET('US/Eastern'), TZ_OFFSET('Canada/Yukon'), TZ_OFFSET('Europe/London') FROM DUAL;

9) FROM_TZ

• Display the TIMESTAMP value '2000-03-28 08:00:00' as a TIMESTAMP WITH TIME ZONE value for the 'Australia/North' time zone region.

SELECT FROM_TZ(TIMESTAMP'2000-07-12 08:00:00', 'Australia/North') FROM DUAL;

10) TO_TIMESTAMP

• Display the character string '2007-03-06 11:00:00' as a TIMESTAMP value:

SELECT TO_TIMESTAMP ('2007-03-06 11:00:00','YYYY-MM-DD HH:MI:SS') FROM DUAL;

11) TO_YMINTERVAL

• Display a date that is one year and two months after the hire date for the employees working in the department with the DEPARTMENT_ID 20.

SELECT hire_date, hire_date + TO_YMINTERVAL('01-02') AS HIRE_DATE_YMININTERVAL FROM employees WHERE department_id = 20;

12) TO_DSINTERVAL


Display a date that is 100 days and 10 hours after the hire date for all the employees.

SELECT last_name, TO_CHAR(hire_date, 'mm-dd-yy:hh:mi:ss') hire_date, TO_CHAR(hire_date + TO_DSINTERVAL('100 10:00:00'), 'mm-dd-yy:hh:mi:ss') hiredate2 FROM employees;

13) Daylight Saving Time

• First Sunday in April

– Time jumps from 01:59:59 AM to 03:00:00 AM.

– Values from 02:00:00 AM to 02:59:59 AM are not valid.

• Last Sunday in October

– Time jumps from 02:00:00 AM to 01:00:01 AM

– Values from 01:00:01 AM to 02:00:00 AM are ambiguous because they are visited twice.

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
