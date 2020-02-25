---
layout: post

title: UNIX - Commands - Files, kernel Interact, Env Variables, Work with vi
---



{{ page.title }}

================


19) Managing Files with the shell

cat filename - outputs contents of filename to display

less filename - Allows scrolling while reading contents of filename

mv file1 file2 - Renames file1 to file2

mv file dir-Moves file to specified directory

cp file1 file2 - Copies file1 and creates file2

rm file - Deletes file

rmdir dir - deletes directory(if empty)

grep string files - Searches through files and displays lines containing matching strings

man grep

20) Working with Compressed files

bunzip2 - Expands a compressed file

bzip2 - Compresses or expands files and directories

gunzip - Expands a compressed file

gzip - Compresses or expands files and directories

tar - creates, expands or lists the contents of compressed or uncompressed file or directory archives known as tape archives or tarballs

To create a compressed archive of a directory,use tar's czf options

tar czf dirname.tgz dirname

To list the contents of the compressed archive, substitute the c option with letter t

tar tzf archive

if many files are in the archive

tar tzf archive | less

To expand the contents of a compressed archive, use tar's zxf options.

21) Use Essential commands from the /bin and /sbin directories

The /bin contains the essential commands used by the system for running and booting linux

/sbin :-In general only the root operator uses the commands in /sbin directory

22) Use and edit files in the /etc directory

fstab - The file system table is a text file listing each hard drive,CD-ROM,floppy or other storage device attached to your PC. Nearly all entries in fstab can be maipulated by root using the mount command.

modprobe.d/-This folder holds all the instructions to load kernel modules that are required as part of the system startup and replaces the historic modprobe.conf file.

passwd :- The list of users for the system, along with user account information.of

shells :- A list of approved shells.

23) Protect the contents of user directories-/home

The most important data on a linux system resides in the user's directories, found under the /home directory.

24) Use the contents of /proc directory to interact with the kernel

The contents of the /proc directory is created from memory and exists only while Linux is running.

free command obtains its information from a file named meminfo

cat /proc/meminfo

-To turn on kernel protection against one type of denial of service attack known as SYN flooding, use the echo command to send the number 1(one) to the following /proc path.

sudo echo 1>/proc/sys/net/ipv4/tcp_syncookies

- getting CPU information, such as family, type and speed from /proc/cpuinfo

- viewing important networking information under /proc/net, such as active interfaces information under /proc/net/dev,routing information in /proc/net/route and network statistics in /proc/net/netstat

- reporting media mount point information via USB; for example, the linux kernel reports what device to use to access files(such as /dev/sda) if a USB camera or hard drive is detected on the system. You can use the dmesg command to see this information.

24) Work with shared data in the /usr directory

The /usr directory contains software applications, libraries and other types of shared data for use by anyone on the system.   

25) Temporary File storage in the /tmp directory.

The /tmp directory is used for temporary file storage

26) Access variable data files in the /var directory

The /var directory contains subdirectories used by various system services for spooling and logging. Many of these variable data files   such as print spooler queues, are temporary, whereas others, such as system and kernal loas, are renamed and rotated in use.

27) Using Environment variables

A number of in-memory variables are assigned and loaded by default when the user logs in. These variables are known as shell environment variables, which can be used by various commands to get information about your environment, such as the type of system you are running, your home directory and the shell in use.

PWD :- To provide the name of the current working directory.

USER :- To declare the user's name, such as andrew.

LANG :- To set language defaults, such as english.

SHELL :- To declare the name and location of the current shell, such as /bin/bash.

PATH :- To set the default location of executable files, such as /bin, /usr/bin and so on.

TERM :- To set the type of terminal in use, such as vt100, which can be important when using screen-oriented programs, such as text editors.

MACHINE :- To declare system type, system architecture and so on.

$env

28) Working with vi

Cursor movement :- h, j, k ,l (left, down, up, right) 

Delete character :- x

Delete line :- dd

mode toggle :- Esc, insert(or i)

Quit :- q

Quit without saving :- q!

Run a shell command :- sh (use 'exit' to return)

Save file :- w

Text search- /
