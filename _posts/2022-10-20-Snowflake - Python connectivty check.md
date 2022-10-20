---
layout: post

title: Snowflake - Python connectivty check
---



{{ page.title }}

================


import snowflake.connector

# Gets the version

ctx = snowflake.connector.connect(

    user='****',
    
    password='*****',
    
    account='dev'
    
    )

cs = ctx.cursor()

try:

    cs.execute("SELECT current_version()")
    
    one_row = cs.fetchone()
    
    print(one_row[0])
    
finally:

    cs.close()

ctx.close()
