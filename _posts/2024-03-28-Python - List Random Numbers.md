---
layout: post

title: Python -  List Random Numbers
---


{{ page.title }}

================

import random

def randomList(n): 

  s = [0] * n 

  for i in range(n): 

    s[i] = random.random() 

  return s 

print(randomList(8))
