---
layout: post

title: UNIX: Commands
---

1)	dmesg 

ubuntu has a command that enables you to see detailed messages that are output directly by the operating system.

$ dmesg > dmesg.txt

2) less dmesg.txt

3) Copy command

$ cp file file.backup

4) sudo command. 

This command is used in front of other commands to tell ubuntu that you want to run the specified command with super user powers.

$ sudo command commandoptions

the following command will open your xorg.conf file in vi and enables you to make any changes as the super user before being able to save it.

$ sudo vi /etc/x11/xorg.conf

the following command tells the package management utility apt -get to check in with the configured repositories and check for any updates for installed software.

$ sudo apt -get update

To upgrade the software

$ apt -get dist -upgrade

5) Working with VI

$vi file.txt

•	Cursor movement - h,j,k,l(left,down,up and right)
•	Delete character - x
•	Delete line - dd
•	Mode - Esc, Insert(or i)command
•	Quit - q
•	Quit without saving - q!
•	Run a shell command - sh(use 'exit')
•	Save file - w
•	Text search - /

6) Working with Permissions

•	You can examine the default permissions for a file you create by using the unmask or touch command

$ touch file
$ ls -l file

In the above example, the touch command is used to quickly create a file. The ls commands then reports on the file, displaying information(from left to right) in the first field of output(such as -rw-r--r--)

•	Permissions: Read, write and execute permissions for the owner, group and all others on the system.

•	Number of links to the file: The number one(1) designates that there is only one file, whereas any other number indicates that there might be one or more hard-linked files. Links are created with the ln command.

•	The owner: The account that created or owns the file; you can change this designation using the chown command.

•	The group: The group of users allowed to access the file; you can c hange this designation by using the chgrp command.

•	File size and creation/modification date: The last two elements indicate the size of the file in bytes and the date the file was created or last modified.

8) Assigning Permissions

Under linux, permissions are grouped by owner, group and others with read, write and execute permission assigned to each.

Owner Group Others
rwx   rwx   rxw

Permissions can be indicated by mnemonic or octal characters. Mnemonic characters are

•	r : indicates permissions for an owner, member of the owners group, or others to open and read the file.
•	w : indicates permission for an owner, member of the owners group or others to open and write to the file.
•	x : indicates permission for an owner, member of the owners group or others to execute the file.

Many users prefer to use numeric codes, based on octal(base 8) values, to represeent permissions. here's what these values mean.

-4 indicates read permission
-2 indicates write permission
-1 indicates execute permission.

9) Directory Permissions

Directories are also files under Linux. For example, again use the ls command to show permissions like this:

$ mkdir foo
$ ls -ld foo

drwxrwxr-x

This shows that the owner and group members can read and write to the directory and, because  

In the above example, the mkdir command is used to create a directory. The ls command and its -ld option is used to show permissions and other information about the directory.

The mnemonic forms of chmod's options(when used with plus,+, character to add or a minus sign,-, to take away) designate the follwoing.

•	u : Adds or removes user (owner) read, write or execute permissions.
•	g : Adds or removes group read, write, or execute permissions
•	o : Adds or removes read, write, or execute permission for others not in a file group
•	a : Adds or removes read, write,or execute permissions for all users
•	r : Adds or removes read permission
•	w : Adds or removes write permission
•	x : Adds or removes execution permission

for eg: if you create a file, such as readme.txt, the file will have default permissions(set by the unmask setting in /etc/bashrc) of

-rw-rw-r-- 1 andrew andrew 12 Jan 2 16:48 readme.txt

As you can see, you and members of your group can read and write the file.Anyone else can only read the file. You can remove all write permission for anyone by using chmod, the minus sign, and aw like so:

$chmod -aw readme.txt
$ls -l readme.txt

Now, no one can write to the file(except you, if the file is in your home or /tmp directory because of directory permissions.). To restore read and write permission for only you as the owner, use the plus sign and the u and rw options like so

$chmod u+rw readme.txt
$ls -l readme.txt

You can also use the octal form of the chmod command, for eg:, to modify a file's permissions so that only you, the owner can read and write a file. Use the chmod command and a file permission of 600, like this:

$ chmod 600 readme.txt
