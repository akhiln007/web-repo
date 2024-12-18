---
layout: post

title: Python -  String Split
---



{{ page.title }}

================

tale='This is the best of times.'

print(tale.split())

s='Mississippi'

print(s.split('i'))

print(s.split())  # no white space


line = 'Go:  Tear some strings apart!'

seq = line.split()

seq

print(line.split(':'))

print(line.split('ar'))

lines = 'This includes\\nsome new\\nlines.'

print(lines.split())
