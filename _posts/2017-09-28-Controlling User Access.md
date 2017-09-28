---
layout: post
title: SQL - Controlling User Access
---

{{ page.title }}
================

1) Privileges

• Database security:

– System security

– Data security

• System privileges: Performing a particular action within the database

• Object privileges: Manipulating the content of the database objects

• Schemas: Collection of objects such as tables, views, and sequences

2) System Privileges

• More than 100 privileges are available.

• The database administrator has high-level system privileges for tasks such as:

– Creating new users

– Removing users

– Removing tables

– Backing up tables

3) Creating Users

CREATE USER demo IDENTIFIED BY demo;

4) User System Privileges

• After a user is created, the DBA can grant specific system privileges to that user.

GRANT create session, create table, create sequence, create view TO demo;

5) Creating and Granting Privileges to a Role

• Create a role:

CREATE ROLE manager;

• Grant privileges to a role:

GRANT create table, create view TO manager;

• Grant a role to users:

GRANT manager TO BELL, KOCHHAR;

6) Changing Your Password

• You can change your password by using the ALTER USER statement.

ALTER USER demo IDENTIFIED BY employ;

7) Object Privileges

• Object privileges vary from object to object.

• An owner has all the privileges on the object.

• An owner can give specific privileges on that owner’s object.

• Grant query privileges on the EMPLOYEES table:

GRANT select ON employees TO demo;

• Grant privileges to update specific columns to users and roles:

GRANT update (department_name, location_id) ON departments TO demo, manager;

8) Passing On Your Privileges

• Give a user authority to pass along privileges:

GRANT select, insert ON departments TO demo WITH GRANT OPTION;

• Allow all users on the system to query data from Alice’s DEPARTMENTS table:

GRANT select ON alice.departmentsTO PUBLIC;

9) Revoking Object Privileges

• You use the REVOKE statement to revoke privileges granted to other users.

• Privileges granted to others through the WITH GRANT OPTION clause are also revoked.

REVOKE select, insert ON departments FROM demo;
