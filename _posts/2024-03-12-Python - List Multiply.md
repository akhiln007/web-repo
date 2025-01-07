---
layout: post

title: Python -  List Multiply
---



{{ page.title }}

================


def multiplyAll(numList, multiplier):    #1
    '''Return a new list containing all
    of the elements of numList, each
    multiplied by multiplier.  For example:

    >>> print(multiplyAll([3, 1, 7], 5))
    [15, 5, 35]
    '''

    newList = list()                     #2

    for num in numList:                  #3

        newList.append(num*multiplier)   #4

    return newList                       #5

print(multiplyAll([3, 1, 7], 5))         #6
