---
layout: post

title: Python -  Interactive For Loop
---



{{ page.title }}

================

lines = list() 

n = int(input('How many lines do you want to enter? ')) 

for i in range(n): 

    line = input('Next line: ') 

    lines.append(line) 
 
print('Your lines were:')  # check now 

for line in lines: 

    print(line) 
   
