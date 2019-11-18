---
layout: post

title: UNIX - Commands
---



{{ page.title }}

================

75) Environment Variables

Certain elements of the Unix world, including the command line interpreter itself can be influenced by a collection of settings known as “the environment”. Each of these settings is individually referred to as an “environment variable”.
We can see the entire environment with the command, env. This produces one line of output for each setting, shown in the form 

VARIABLE=value

$env | more

We can search for the string “TERM” (all upper case) in the output of env by piping to the grep command. We see that the TERM environment variable is set to xterm and the COLORTERM variable is set to gnome-terminal

The terminal window is a gnome terminal window. This is a modern version of an old sort of terminal window called an xterm. Most programs use the value of the TERM environment variable to work out what sort of terminal it is and therefore how to talk to it.

Running env and grepping the results is slow and inefficient. There is a simple mechanism to determine the value of any variable. Recall that the echo command repeats its arguments only after the shell has rewritten them (as happened with filename globbing). The shell also has a syntax for converting the names of variables into their corresponding values.

$ echo “${TERM}”

Just this one will show you a short cut. In this specific case you could have got away with just this:

$ echo $TERM

But rather than explain when you do and don’t need the double quotes and when you do and don’t need the braces (curly brackets) we will get into the good habit of always using them.

You do always need the dollar character, though. It is the signal that triggers the conversion from variable name to variable value.

$ echo TERM
41) The PATH environment variable

Almost all the commands in unix correspond to a file containing the instructions for that command, typically in the computer’s machine code. You can find out what file a command corresponds to with the “type” command.

$ type more
But how did the shell know to look in the directory “/bin” for a file called “more”. 

The PATH environment variable has as its value a list of directories separated by colons. This is the list of directories the shell will go looking in.

$ echo “${PATH}”

Because it takes time to search through each of these directories the shell remembers where it found each command after the first time it uses it successfully. This is a process called “hashing”.(The sort of record the shell uses to remember this information is called a “hash table”). If we use more and then ask about it again, we get a slightly different answer.

76) The PS1 environment variable

The “PS1” environment variable controls the prompt the shell uses. The prompt we have seen so far looks like this

 

and contains the login id, machine name and the current working directory. Now, we look at the PS1 environment variable. 

$ echo “${PS1}”

 

In the PS1 environment variable the backslash is used to mark ordinary characters as having special meaning.

\h    :- The machine name, also known as host name     
\w    :- The name of the current working directory.
\$    :- This is just the same as “$”, if you are not the super user. It changes to “#” if you are.

There are many other special codes like this. For eg: “\t” gives the time.

77) The HOME environment variable

This identifies your home directory and where the cd command takes you if it is given no argument.

$ echo “${HOME}”

78) Remote access to other unix systems

Unix systems typically offer a secure mechanism to login to another system you have an account on. The command for this is “ssh”(secure shell) and as the name “shell” suggests it gives a command line on the remote system. 

The first part of ssh’s security is to check that you are connecting to the system you think you are. In the ssh world every machine has a “fingerprint”. This appears as a sequence of numbers(expressed base 16 just to make it look more bizarre) which can be securely checked from a workstation(like your PC) which has never made contact with it before. 

79) Remote login between cooperating systems

We connect to the system soup.linux.pwf.cam.ac.uk with the command “ssh soup.linux.pwf.cam.ac.uk” 

80) File Transfer

In addition to logging on to remote systems, we may also want to transfer files to or from them. In addition to ssh(“secure shell”) there is a related program “scp” (“secure copy”). This behaves in exactly in same way as cp except that one of the target or destination is actually a reference to a remote system. There is also an “sftp” program which is an interactive file transfer program that lets you navigate the far end.

81) Fetching Files and directories

There is a file on the machine smaug.linux.pwf.cam.ac.uk called “/tmp/fetch.txt”. To fetch it into the current working directory we could run the following command.

$ scp codeability.org.in:/tmp/fetch.txt fetch.txt

Note: How we define a file on a remote computer: machine_name:file_path with a colon separating the two components.

Just as with ssh, scp assumes you have the same login id on the remote system as on the local one. If you have a different name on the remote system then you specify with as you did for ssh, with “user@” before machine_name:file_path element. So if your remote user id was “bob”, you would run the command.

$ scp akhil@codeability.org.in:/tmp/fetch.txt fetch.txt
If we are happy for the file name to remain the same there is a trick to save the on the typing. We can say “Copy it into this directory” in which case the copy will leave it with the same file name.

$ scp akhil@codeability.org.in:/tmp/fetch.txt .

Recall that “.” means the current directory.

We can rename the file by just giving a different name as the second argument.

$ scp akhil@codeability.org.in:/tmp/fetch.txt new_fetch.txt

To fetch a directory and everything in it, we must specify a recursive copy, just as we had to do to copy a directory within the system. Unfortunately, the scp program hasn’t moved to the modern upper case “-R” option for recursion. So we have to use the lower case “-r”

$ scp -r akhil.linux.codeability.org.in:/tmp/fetchable. 
