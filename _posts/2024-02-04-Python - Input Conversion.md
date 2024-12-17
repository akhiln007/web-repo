---
layout: post

title: Python -  Input Conversion
---



{{ page.title }}

================

'''Conversion of strings to int before addition'''

xString = input("Enter a number: ")

x = int(xString)

yString = input("Enter a second number: ")

y = int(yString)

print('The sum of ', x, ' and ', y, ' is ', x+y, '.', sep='')

'''Two numeric inputs, with immediate conversion'''

x = int(input("Enter a number: "))

y = int(input("Enter a second number: "))

print('The sum of ', x, ' and ', y, ' is ', x+y, '.', sep='')

'''Two numeric inputs, explicit sum'''

x = int(input("Enter an integer: "))

y = int(input("Enter another integer: "))

sum = x+y

print('The sum of ', x, ' and ', y, ' is ', sum, '.', sep='')
