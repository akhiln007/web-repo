---
layout: post

title: Snowflake - Create Snowflake Objects
---



{{ page.title }}

================


1. Creating a Database

Create the emp database using the CREATE DATABASE command:

create or replace database emp;

Note that you do not need to create a schema in the database because each database created in Snowflake contains a default schema named public.

Also, note that the database and schema you just created are now in use for your current session.

select current_database(), current_schema();

2. Creating a Table

Create a table named emp_basic in emp.public using the CREATE TABLE command:

create or replace table emp_basic (
  first_name string ,
  last_name string ,
  email string ,
  streetaddress string ,
  city string ,
  start_date date
  );

3. Creating a Virtual Warehouse

Create an X-Small warehouse named emp_wh using the CREATE WAREHOUSE command:

create or replace warehouse emp_wh with
  warehouse_size='X-SMALL'
  auto_suspend = 180
  auto_resume = true
  initially_suspended=true;

Note that the warehouse is not started initially, but it is set to auto-resume, so it will automatically start running when you execute your first SQL command that requires compute resources.

Also, note that the warehouse is now in use for your current session. This information is displayed in your SnowSQL command prompt, but can also be viewed using the following context function:

select current_warehouse();

