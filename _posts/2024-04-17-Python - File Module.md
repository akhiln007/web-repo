---
layout: post

title: Python -  File Module
---


{{ page.title }}

================

def linecount(filename):

    count = 0

    for line in open(filename):

        count += 1

        return count

print(linecount('L10.7_FileModule.py'))
