---
layout: post

title: UNIX - Commands
---



{{ page.title }}

================


29) File Permissions

For any file or directory, permissions can be established in three categories: user, group and global. The commands used to change the group, user, or access permissions of a file or directory.

- chgrp:- Changes the group ownership of a file or directory.

- chown:- Changes the owner of a file or directory.

- chmod:- Changes the access permissions of a file or directory.

30) Managing Groups

All the groups are listed in /etc/group file

$sudo cat /etc/group

31) Group Management Tools

  The most commonly used group management command-line tools

- groupadd:- This command creates and add a new group.

- groupdel:- This command removes an existing group.

- groupmod:- This command creates a group name or GID's but doesn't add or delete members from a group.

- gpasswd:- This command creates a group password.

- useradd -G:- The -G argument adds a user to a group during the initial user creation.

- usermod -G:- This commands allows you to add a user to a group, so long as the user is not logged in at the time.

- grpck:- A command for checking the /etc/group files for typos.

* Add a new group with the groupadd command;

#groupadd dvdrw

* Change the group ownership of the device to the new group with the chgrp command:

# chgrp dvdrw /dev/scd0

* Add the approved user to the group with the usermod command.

# usermod -G dvdrw john

* Make user john the group administrator with the gpasswd command so that she can add new users to the group

# gpasswd -A john

32) Managing Users

Most frequently used commands to manage users are

-useradd: To add a new user account to the system.

-useradd -D: This command sets the system defaults for creating the user's home directory, account expiration date, default group and command shell.

The set of files initially used to populate a new user's home directory are kept in /etc/ske1.

-userdel: This command completly removes a user account.

-passwd: This command updates the "authentication tokens" used by the password management system.

-To lock a user out of his account, use 

# passwd -l username

-usermod: This command changes several user attributes. The most commonly used arguments are -s to change the shell and -u to change the UID.

-chsh: This command changes the user's default shell. For ubuntu, the default shell is /bin/bash, known as the Bash or Bourne Again shell.

33) Adding new users

#useradd akhil -p STitcher -s /bin/zsh -u 1002

34) Monitoring user activity on the system.

The w commands tells the sysadmin who is logged in and where he is logged in and what he is doing. The w command can be followed by a specific user's name to show only that user.

The ac command provides information about the total connect time of a user measured in hours. It accesses the /var/log/wtmp file for the source of its information.

35) Managing Passwords

The password file is /etc/passwd, and it is the database file for all users on the system. The format of each line is as follwos.

username:password:uid:gid:gecos:homedir:shell

$cat /etc/passwd

$cat /etc/shadow

36) w 

The command “w” will show who is logged in and where

$ w

 

The letters “TTY” in W’s output stand for “Teletype”. This was the name of the old, clunky paper printing terminals that used to be plugged into the backs of the old mainframe computers. Today we don’t have that set up but instead we have multiple teletypes all provided through the same console and switched between using the [Ctrl]+[Alt]+[Fn] key combinations.

The teletype “tty2” corresponds to [Ctrl]+[Alt]+[F2] and “tty3” corresponds to [Ctrl]+[Alt]+[F3]. The seventh teletype(tty7) is dedicated to the graphical interface managed by a program called gnome-session. This is why you use [Ctrl]+[Alt]+[F7] to return to the graphical environment.

The graphical terminal windows are not “real” teletypes. These are managed by a “pseudo-terminal service”, or pts for short. The first two terminal windows you create are assigned pts/0 and pts/1 respectively.

37) who 

Show who is logged on

 

