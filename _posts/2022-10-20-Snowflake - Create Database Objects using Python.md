---
layout: post

title: Snowflake - Create Database Objects using Python
---



{{ page.title }}

================

import snowflake.connector

import os as os


USER=os.getenv('sf_user')

PASSWORD=os.getenv('sf_password')

ACCOUNT=os.getenv('sf_account')

# Connects to database

conn = snowflake.connector.connect(

    user=USER,
    
    password=PASSWORD,
    
    account=ACCOUNT
    
    )

cur = conn.cursor()

try:

    print(cur.execute("SELECT current_version()"))
    
    conn.cur.execute("CREATE WAREHOUSE IF NOT EXISTS SO_PUB_DEV_WH")
    
    conn.cur.execute("CREATE DATABASE IF NOT EXISTS SO_PUB_DEV")
    
    conn.cur.execute("USE DATABASE SO_PUB_DEV")
    
    conn.cur.execute("CREATE SCHEMA IF NOT EXISTS SO_STAGING")
    
finally:

    cur.close()
    
conn.close()
