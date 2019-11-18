---
layout: post

title: UNIX - Commands
---



{{ page.title }}

================

82) Sending files and directories

To send data rather than to fetch it we simply use the same syntax for specifying a remote file but on the second argument rather than the first.

To copy a file from the current working directory to a remote location, we specify it like this

$ scp newdata.txt smaug.linux.pwf.cam.ac.uk:/tmp/y250_data.txt

83) Interactive File Transfer

$sftp linux.pwf.cam.ac.uk

sftp> pwd

The unix command pwd in the sftp program gives information about the remote end. To get the local working directory, use the sftp-only command “lpwd” (“local pwd”)

sftp> lpwd

sftp> lls

sftp> put newdata.txt y250_example.txt

sftp> get fetchme.txt another.txt

To exit the sftp program, either enter [Ctrl]+[D] or the command “quit”. 

sftp> quit

A full set of sftp commands is given by the sftp command “help”.

84) To connect from windows machine to unix machine, use putty

85) To transfer files from windows machine to unix machine, use winscp

86) Trivial Shell scripts

We will open a plain text editor and enter a few trivial shell commands into it. Save the file as commands.sh in our home directory. The following is what should go in the file.

pwd
date
ls -l
cd “Unix Intro”
ls -l

Launch a terminal window. Recall that the name of our shell is “bash”. That’s also the command to run another one of these command line interpreters.

We run the command “bash commands.sh”

$ bash commands.sh

Recall that unix has three types of permission of a file, labelled with “rwx”: a file can be readable, writable and executable. At the moment this file is only readable and writable by us.

$ ls -l commands.sh

We will make it executable by changing its permissions(also known as its “mode”) with the “chmod” command(“change mode”). The syntax of this command is an extreme example of unix complex conciseness.

$ chmod a+x commands.sh

The a+x means “for all classes of user(owner, group number, other) add (+) the execute permission.”

The commands.sh file is now ready to be executed, but the shell will never find it because your home directory is not on your PATH and that’s where the shell looks. We can tell it where to look by giving the exact filename for the command so that it doesn’t have to go looking.

$ /home/y250/commands.sh

Its awkward having to keep track of the directory the file it is in. Recall that the directory “.” means “this directory”. We typically use that to tell the shell to run a command from a file this directory.

$ ./commands.sh

There is a traditional place for personal, “quickie” shell scripts to go. That is in a directory called “bin” in your home directory. 

bin stands for binaries. Once upon a time there was no scripts and every program had to be compiled into a binary executable file.

There is one last change we ought to make for a proper shell script. Scripts can be written in various languages, not just shell.  If there’s no special instructions then the operating system assumes that it is in shell. This is what happened with our script. However it traditional to be explicit.

The “special instructions” lie on the first line. It start with “#!” followed by the full path to the interpreter whose language the script is written in. So, if we wanted to be explicit about the shell, we would start with “#! /bin/bash” as the first line. 

#! /bin/bash

# My first shell script !

pwd
date
ls -l
cd “Unix Intro”
ls -l

Incidentally, any scripting language that uses “#” as its comment character can have scripts defined this way. So python(file /usr/bin/python) has scripts starting with “#! /usr/bin/python”, Perl has “#! /usr/bin/perl” etc
