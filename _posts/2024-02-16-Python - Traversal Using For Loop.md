---
layout: post

title: Python -  Traversal Using For Loop
---



{{ page.title }}

================

#First

for count in [1, 2, 3]:

    print(count)

    print('Yes' * count)

#Second    

for count in [1, 2, 3]:

    print(count)

    print('Yes' * count)

print('Done counting.')

for color in ['red', 'blue', 'green']:

    print(color)

#Third

for count in [1, 2, 3]:

    print(count)

    print('Yes' * count)

    print('Done counting.') # changed so indented

for color in ['red', 'blue', 'green']:

    print(color)

#Fourth

''' use a function to number the entries in any list'''

def numberList(items):

    '''Print each item in a list items, numbered in order.'''

    number = 1

    for item in items:

        print(number, item)

        number = number + 1

def main():

    numberList(['red', 'orange', 'yellow', 'green'])

    print()

    numberList(['apples', 'pears', 'bananas'])

main()

#Fifth

def listOnOneLine(items):

    for item in items:

        print(item, end=' ')

listOnOneLine(['apple', 'banana', 'pear'])

print('This may not be what you expected!')

#Sixth

def listOnOneLine(items):

    for item in items:

        print(item, end=' ')

    print()

listOnOneLine(['apple', 'banana', 'pear'])

print('This is probably better!')
