---
layout: post

title: Python -  Find Function
---



{{ page.title }}

================

2024-02-20-Python - Find Function.md

def find(str, ch): 

  index = 0 

  while index < len(str): 

    if str[index] == ch: 

      return index 

    index = index + 1 

  return -1 

s = 'Mississippi'

print(s.find('i'))

print(s.find('si'))

print(s.find('sa'))

print(s.find('si',4))


line='Hello, there!'

print(line.find('e'))

print(line.find('he'))

print(line.find('e', 10))

print(line.find('he', 10))

vals=[5, 7, 9, 22, 6, 8]

print(vals[1])

print(vals[-2])

print(vals[1:4])
