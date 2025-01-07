---
layout: post

title: Python -  List Comprehension
---


{{ page.title }}

================

new_list = [x for x in range(1,6)]

print(new_list)

doubles = [x*2 for x in range(1,6)]

print(doubles)

# doubled numbers that are evenly divisible by three

doubles_by_3 = [x*2 for x in range(1,6) if (x*2)%3 == 0]

print(doubles_by_3)

cubes_by_four=[y**3 for y in range(1,11) if ((y**3)%4)==0]

print(cubes_by_four)
