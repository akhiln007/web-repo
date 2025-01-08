---
layout: post

title: Python -  Dictionary Letter Counts
---


{{ page.title }}

================

letterCounts = {} 

for letter in "Mississippi":

    letterCounts[letter] = letterCounts.get (letter, 0) + 1 
    
print(letterCounts)
