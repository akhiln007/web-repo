---
layout: post

title: Python -  Encapsulation and Generalization Tables
---



{{ page.title }}

================

def printMultiples(n, high): 

  i = 1 

  while i <= high: 

    print(n*i, '\t') 

    i = i + 1 
   

def printMultTable(high): 

  i = 1 

  while i <= high: 

    printMultiples(i, high) 

    i = i + 1 

printMultTable(7)
