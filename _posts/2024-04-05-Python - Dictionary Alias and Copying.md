---
layout: post

title: Python -  Dictionary Alias and Copying
---


{{ page.title }}

================

opposites = {'up': 'down', 'right': 'wrong', 'true': 'false'}
 
alias = opposites 

copy = opposites.copy() 

print(opposites)

print(alias)

print(copy)

alias['right'] = 'left' 

print(alias['right'])

print(opposites['right'])

print(copy['right'])

copy['right'] = 'privilege' 

print(alias['right'])

print(opposites['right'])

print(copy['right'])
