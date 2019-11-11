---
layout: post

title: UNIX - Commands
---



{{ page.title }}

================

66) Repeating the command line

$ echo one two three

The echo command repeats whatever you give it as arguments.

67) bc - (basic calculator)

$bc 2+4

[Ctrl]+[D]   To exit

68) Redirecting data and piping commands

The “cat” command is a program for cancatenating one or more plain text files. You can concatenate a single file. But it is rarely useful.

$ cat abc.txt def.txt ghi.txt

69) Standard output

All the unix commands that deal with linear data (such as plain text) typically spit their output to the terminal by default where that linear stream of data typically rushes past you. This output stream is known technically as “standard output” and by default a program’s standard output goes to terminal where it is being run. But it can be redirected.

$cat abc.txt def.txt > combined.txt

The redirection “>” has taken the standard output of the cat command and redirected it from the terminal into a file combined.txt. The redirection overwrites any content of the file that was previously there.

There is a variant of “>” which appends to the end of any pre-existing file(and which still creates the file if it does not): “>>”

$ cat ghi.txt >> combined.txt

70) Standard Input:- 

If a command takes a file name as an argument then it is going to get its data from that file, but those commands  can often also take their input from the keyboard directly. In this case we use [Ctrl]+[D] to mark “end of input”.

We already met wc

$wc abc.txt

We can also tell it to get its input from its standard input(keyboard) by omitting any filename.

$ wc I am learning unix to start the shell scripting. [Ctrl]+[D]

Because  [Ctrl]+[D] is potentially so dangerous, there is a special shell syntax to say “end the input with this”

$wc <<END

I am learning unix to start the shell scripting.

END

Also note that there is nothing special about “END”. It is just the string of characters that follows “<<”

There is no need for the end marker to be a word. Punctuation works too and “!” is a traditional marker.

$wc <<!

I am learning unix to start the shell scripting.

!

Finally we can redirect the standard input from a pre-existing file with the “<” redirector. Think of it as an arrow but this time pointing into command rather than out of it.

$wc < command.txt

71) Piping:- 

The full power of standard input and output only becomes clear when we combine the two. We can take the standard output of one command and feed it directly into the standard input of a second. This simple construction allows us to combine unix commands in very powerful ways.

It is done by placing the “|” character between the two commands.


$ cat lorem.txt combined.txt | wc


$ grep -iw rum story.txt | more


A very common use of piping is to the more command. If a command’s output is too long to fit on a single screen then piping it through more paginates the output.

72) File Name Globbing

The next command line trick we will see is called “wild carding” or “globbing”. This allows us to express a set of files without having to list them all manually.

Asterisk:- Observe this use of the echo command in the work directory.

$ echo abc.txt combined.txt def.txt ghi.txt lorem.txt 

The trick behind globbing is that the shell will take certain special characters and convert them into lists of filenames. So, for eg, the expression “*.txt” is converted into the list of files that end in “*.txt”. The “*” stands for anything.

$ echo *.txt

Globbing does not work inside quotes or if the asterisk is preceded by a backslash.(Remember that this makes characters special to the shell, like space, ordinary parts of file name. Well it works on asterisks too.)

$ echo “*.txt”

$ echo ‘*.txt’

$ echo \*.txt

Also if a glob(“wild card”) doesn’t match anything it passes through unaltered.

$ echo *.foo

*.foo

73) Question Mark

There are other globs. The asterisk, “*”, expands into “anything”. The question mark, “?”, expands into any one character.

$ echo abc.t*

$ echo abc.t?

$ echo abc.t???

74) Square Brackets

The last glob allows us to say “any one character from this set” or even “any one character not from this set”.

The glob “[aeiou]” means “any one of ‘a’,’e’,’i’,’o’,’u’ ”

$ echo abc.t[xyz]t

$ echo abc.t[abc]t

We can negate this membership with the syntax “[^aeiou]” to mean “any one character that is not ‘a’,’e’,’i’,’o’,’u’”

$ echo abc.t[^xyz]t

$ echo abc.t[^abc]t

The set of new globs

[:alnum:]   Any alphabetic character(upper or lower case) or any digit.

[:alpha:]    Any alphabetic character(upper or lower case).

[:blank:]    Any horizontal white space (space or tab,essentially)

[:digit:]      Any of the ten digits

[:lower:]    Any lower case alphabetic character

[:upper:]    Any upper case alphabetic character
