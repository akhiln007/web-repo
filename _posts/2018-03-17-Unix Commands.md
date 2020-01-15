---
layout: post

title: UNIX - Commands - Permissions, root, users, shutdown, docs, man pages, GNU Commands
---



{{ page.title }}

================

10) Understanding Set User ID and Set Group Id permissions

Another type of permission is "set user Id", known as suid, and "set group ID"(sgid) permissions. These settings, when used in a program, enable any user running that program to have program owner or group owner permissions for that program. These settings enable the program to be run effectively by anyone, without requiring that each users permissions be altered to include specific permissions for that program.

One commonly used program with suid permissions is the passwd command.

$ ls -l /usr/bin/passwd

This setting allows normal users to execute the command(as root) to make changes to a root-only accessible file, /etc/passwd.

You can also assign similar permission with chfn command. This command allows users to update or change finger information in /etc/passwd.

Savvy Linux system administrators keep the number of suid or guid files present on a system to a minimum. The find command can be used to display all such files on your system.

$ find / -type f -perm +6000 -exec ls -l {} \;

11) Working as root

Super user permissions are required in part because of the restrictive file permissions assigned to important system configuration files. You must have root permission to edit these files or to access or modify certain devices.

When you work in root, you can destroy a running system with simple invocation of the rm command like this

$rm -fr /

This command line not only deletes files and directories, but also could wipe out file systems on other partitions and even remote computers.

Linux comes with a command named su that enables you to run one or more commands as root and then quickly returns you to normal user status. for eg. if you would like to edit your systems file system table, you can use the su command like this.

$ su -c "nano -w /etc/fstab"

you can use the sudo in the same way to allow you to execute one-off commands. The above example would look like this,

$ sudo nano -w /etc/fstab

12) Creating Users

When a linux system administrator creates a user, an entry in /etc/passwd for the user is created. The system also creates a directory, labled with the user's username, in the /home directory. For eg: if you create a user named Akhil, the user's home directory is /home/Akhil

To create user:

$ sudo useradd akhil

To create the password

$sudo passwd akhil

To delete user

$sudo userdel -r akhil

13) Shutting down the system

$ sudo shutdown -h now  

or

$sudo shutdown -h 0

To incorporate a timed shutdown and a message to all

$sudo shutdown -h 18:30 "System going down for maintenance" 

Rebooting the system

$ sudo shutdown -r now   

or

$ sudo shutdown -r 0

14) Reading Documentation

You can use the apropos command-for eg, with a keyword such as partition to find commands related to partitioning

$ apropos partition

To find a command and its documentation, you can use the whereis command. For eg, if you are looking for the fdisk command, you can do this

$whereis fdisk

15) Using man pages

To learn more about a command or program, use the man command, followed by the name of the command.

$ man rm

16) Root user

In other Linux distros, you would change to the root user by issuing the command su followed by the root password. This will land you at the root prompt, which is shown as a pound sign(#). To get to a root prompt in ubuntu, you need to execute the command 

sudo -i

17) Basic Linux Directories

/    The root directory

/bin    Essential commands

/boot    Boot loader files, Linux kernal

/dev    Device files

/etc    System configuration files

/home    User home directories

/initrd initial RaM disk boot support(used during boot time)

/lib    Shared libraries, kernal modules

/lost+found    Directory for recovered files(if found after a file system check)

/media    Mount point for removable media, such as DVDs and floppy disks

/mnt    usual mount point for local, remote file systems

/opt    Add-on software packages

/proc    Kernal information, process control

/root    Super-user (root) home.

/sbin    System commands(mostly root only)

/srv    Holds information relating to services that run on your system

/sys    Real-time information on devices used by kernal

/tmp    Temporary files

/usr    Secondary software file hierarchy

/var    Variable data(such as logs); spooled files

18) GNU Commands to search the file system

whereis command:-

Returns the location of the command and its main page.

whatis command:-

Returns a one-line synopsis from the command's main page

locate file:-

Returns locations of all matching files

apropos subject:-

Returns a list of commands related to subject
