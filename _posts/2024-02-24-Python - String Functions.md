---
layout: post

title: Python -  String Functions
---



{{ page.title }}

================

'''Let's take a closer look at why you use len(string) and str(object), but dot notation (such as "String".upper()) for the rest.
Methods that use dot notation only work with strings. On the other hand, len() and str() can work on other data types.'''

s = "Go Gators! Come on Gators!"

print(s[3:9]) # "Gators"

print(s[:2])  # "Go"

print(s[19:]) # "Gators!"

print(s[-7:-2]) # "Gator"

print(s.count("Gator")) # 2

print(s.endswith("Gators")) # False

print(s.endswith("Gators!")) # True

print(s.find("Gator")) # 3

print(s.find("gator")) #-1

print(len(s)) #26

print(s.lower()) #go gators! come on gators!

print(s.replace("Gators","Tigers",1)) #Go Tigers! Come on Gators!

print(s.rfind("Gator")) # 19

print(s.split()) #['Go', 'Gators!', 'Come', 'on', 'Gators!']

print(s.startswith("Go")) # True
