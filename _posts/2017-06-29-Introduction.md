---
layout: post
title: SQL - Introduction
---

{{ page.title }}
================

1) Data

Every organization has some information needs. A library keeps a list of members, books, due dates and fines. A company needs to save information about its employees, departments, and salaries. These pieces of information are called data.

2) Database

A database is an organized collection of information.

3) DBMS

To manage databases, you need a database management system (DBMS). A DBMS is a program that stores, retrieves, and modifies data in database on request. There are four main types of databases: hierarchical, network, relational, and object relational.  

4) Relational Database Concept

Dr. E. F. Codd proposed the relational model for database systems in 1970. It is the basis for the relational database management system (RDBMS). The relational model consists of the following:

– Collection of objects or relations

– Set of operators to act on the relations

– Data integrity for accuracy and consistency

5) Definition of a Relational Database

A relational database uses relations or two-dimensional tables to store information. For example, you might want to store information about all the employees in your company. In a relational database, you create several tables to store different pieces of information about your employees, such as an employee table, a department table, and a salary table.

6) Data Models

Models are the cornerstone of design. Engineers build a model of a car to work out any details before putting it into production. In the same manner, system designers develop models to explore ideas and improve the understanding of database design.

Purpose of Models

Models help communicate the concepts that are in people’s minds. They can be used to do the following:

• Communicate

• Categorize

• Describe

• Specify

• Investigate

• Evolve

• Analyze

• Imitate

The objective is to produce a model that fits a multitude of these uses, can be understood by an end user, and contains sufficient detail for a developer to build a database system.

7) Entity Relationship Model

In an effective system, data is divided into discrete categories or entities. An entity relationship (ER) model is an illustration of the various entities in a business and the relationships among them. An ER model is derived from business specifications or narratives and built during the analysis phase of the system development life cycle. ER models separate the information required by a business from the activities performed within the business. Although businesses can change their activities, the type of information tends to remain constant. Therefore, the data structures also tend to be constant.

8) Benefits of ER Modelling

Documents information for the organization in a clear, precise format

• Provides a clear picture of the scope of the information requirement.

• Provides an easily understood pictorial map for database design.

• Offers an effective framework for integrating multiple applications.

Key Components

• Entity: An aspect of significance about which information must be known. Examples are departments, employees, and orders.

• Attribute: Something that describes or qualifies an entity. For example, for the employee entity, the attributes would be the employee number, name, job title, hire date, department number, and so on. Each of the attributes is either required or optional. This state is called optionality.

• Relationship: A named association between entities showing optionality and degree. Examples are employees and departments, and orders and items


9) SQL

SQL is a standard language for accessing and manipulating databases.

10) What is SQL?

SQL stands for Structured Query Language.

SQL lets you access and manipulate databases.

SQL is an ANSI (American National Standards Institute) standard.

11) What Can SQL do?

SQL can execute queries against a database.

SQL can retrieve data from a database.

SQL can insert records in a database.

SQL can update records in a database.

SQL can delete records from a database.

SQL can create new databases.

SQL can create new tables in a database.

SQL can create stored procedures in a database.

SQL can create views in a database.

SQL can set permissions on tables, procedures, and views.

12) Data manipulation language (DML)

SELECT

INSERT

UPDATE

DELETE

MERGE

13) Data definition language (DDL)

CREATE

ALTER

DROP

RENAME

TRUNCATE

COMMENT

14) Data control language (DCL)

GRANT

REVOKE

15) Transaction control

COMMIT

ROLLBACK

SAVEPOINT


16) Using SQL in Your Web Site

To build a web site that shows data from a database, you will need:

An RDBMS database program (i.e. MS Access, SQL Server, MySQL)

To use a server-side scripting language, like PHP or ASP.

To use SQL to get the data you want.

To use HTML / CSS to style the page.

17) RDBMS

RDBMS stands for Relational Database Management System. RDBMS is the basis for SQL, and for all modern database systems such as MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.

The data in RDBMS is stored in database objects called tables. A table is a collection of related data entries and it consists of columns and rows.

Every table is broken up into smaller entities called fields. The fields in the Customers table consist of CustomerID, CustomerName, ContactName, Address, City and PostalCode. A field is a column in a table that is designed to maintain specific information about every record in the table.

A record, also called a row, is each individual entry that exists in a table. For example, there are 91 records in the above Customers table. A record is a horizontal entity in a table.
A column is a vertical entity in a table that contains all information associated with a specific field in a table.

18) Database Tables

A database most often contains one or more tables. Each table is identified by a name (e.g. "Customers" or "Orders"). Tables contain records (rows) with data.

19) Keep in Mind That...

SQL keywords are NOT case sensitive: select is the same as SELECT

20) Semicolon after SQL Statements

Some database systems require a semicolon at the end of each SQL statement.

Semicolon is the standard way to separate each SQL statement in database systems that allow more than one SQL statement to be executed in the same call to the server.

21) Some of the Most Important SQL Commands

SELECT - extracts data from a database.

UPDATE - updates data in a database.

DELETE - deletes data from a database.

INSERT INTO - inserts new data into a database.

CREATE DATABASE - creates a new database.

ALTER DATABASE - modifies a database.

CREATE TABLE - creates a new table.

ALTER TABLE - modifies a table.

DROP TABLE - deletes a table.

CREATE INDEX - creates an index (search key).

DROP INDEX - deletes an index 
