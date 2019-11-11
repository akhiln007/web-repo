---
layout: post

title: UNIX - Commands
---



{{ page.title }}

================

49) mkdir

To create an empty new directory we use the command, mkdir(“make directory”)

50) Removing directories and files

rm:- To remove a file we can use the rm(“remove”) command.

rmdir:- Empty directories can be removed with the rmdir(“remove directory”).

rmdir -R :- To remove a directory which has content, use with -R(recursive) option.

$ rm -R  test

16) Following is an example of the general case for a unix command

$ ls -la work

command options parameter

51) man 

To print the manual pages for a command.

$ man ls

52) bg 

background jobs

53) fg 

foreground jobs

54) xeyes

55) kill %1

56) kill -kill %3

57) What would the GUI do

We can ask the windowing system to open a file with “whatever application it would have used if we had double clicked on the icon in the graphical interface”. The command to do this is called “gnome -open”

$gnome-open story.txt

58) Touch 

To create an empty file, say akhil.txt, use touch akhil.txt

60) [ctrl]+[R] triggers a backwards search.

61) Clearing the screen

$clear

Suppose we have some command output on the screen already and start to type a command. We can then press [Ctrl]+[L] at that point, to clear the screen but leave the partially typed command.

$ [ctrl]+[L] 

62) Reading plain text file

The classic command for reading a plain text file is called “more”. 

$more akhil.txt

63) Searching plain text file

To search through a plain text file for particular words or phrases, we use the command grep

$grep Rum story.txt

We can search for more than one word by quoting together the phrase to search for.

$grep “Akhil Nair” story.txt

We can tell grep to search for whole words only with the “-w”(word) option.

$grep -w rum story.txt

we can search for “Rum” and “rum” by requesting a case insensitive search with the option “-i”(insensitive)

if we want just the word “rum” but in either case we combine the -i and -w options.

“grep -iw”, ”grep -wi”,  “grep -i -w” and “grep -w -i” are all equivalent.

64) wc -(word count) 

To count the words, lines or even characters.

$wc story.txt

-l for the line count
-w for the word count
-c for the character count

$wc -l story.txt

65) Telling the Time

$date

The date command accepts an argument called a “format string” which controls the looks of the output.

$date +”%d %m %y”
 

The string in quotes after the plus sign is the format string. %d is converted to the day of the month, %m to the numerical month of the year and %y to the year. Characters without preceding percentage characters are simply repeated, like the spaces in the above example.
$date +”%Y %B %d”

 
