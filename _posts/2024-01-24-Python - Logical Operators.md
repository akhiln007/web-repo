---
layout: post

title: Python -  Logical Operators
---



{{ page.title }}

================


#and

x = 10

print(x > 5 and x < 15)

#This returns True because 10 is greater than 5 AND 10 is less than 15.


#or

x = 10

print(x > 5 or x < 2)

#This returns True because one of the conditions are true.

#10 is greater than 5, but 10 is not less than 2.


#not

x = 10

print(not(x > 5 and x < 15))

#This returns False because not reverses the result of and.
