---
layout: post

title: Python -  Encapsulation and Generalization
---



{{ page.title }}

================

def printMultiples(n): 

  i = 1 
  
  while i <= 6: 
  
    print(n*i, '\t') 
    
    i = i + 1 

printMultiples(5) 

def printMultTable(high): 

  i = 1 
  
  while i <= high: 
  
    printMultiples(i) 
    
    i = i + 1 


printMultTable(7)
   
