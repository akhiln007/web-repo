---
layout: post

title: Python -  Print Formatting
---



{{ page.title }}

================


'''Hello to you!  Illustrates format with {} in print.'''

person = input('Enter your name: ')

greeting = 'Hello, {}!'.format(person)

print(greeting)


'''Compare print with concatenation and with format string.'''

applicant = input("Enter the applicant's name: ")

interviewer = input("Enter the interviewer's name: ")

time = input("Enter the appointment time: ")

print(interviewer + ' will interview ' + applicant + ' at ' + time +'.')

print(interviewer, ' will interview ', applicant, ' at ', time, '.', sep='')

print('{} will interview {} at {}.'.format(interviewer, applicant, time))


'''Two numeric inputs, explicit sum'''

x = int(input("Enter an integer: "))

y = int(input("Enter another integer: "))

sum = x+y

sentence = 'The sum of {} and {} is {}.'.format(x, y, sum)

print(sentence)
