---
layout: post

title: UNIX - Commands
---



{{ page.title }}

================

38) uptime 

Tells how long the system has been running.

39) Navigating the file system

 All the elements of a Linux system form a hierarchy called the “file system”. This hierarchy is a tree of folders(typically called “directories” in the unix world) and files containing content.

40) pwd

To know which directory we are in, we use the command pwd, “print working directory”
 

41) ls 

To see what is in the current directory, we use the ls(“list”) command. The directories are coloured blue.

We can get more information from ls about the contents of the directory by asking for its “long” output. We do this by adding the option -l

We can analyse the output of ls -l in detail. It will be explained right to left.

software :- This is the name of file or directory.

Mar 3 10:39  :- This is the date and time of the last update to the file, or the date it was created if it has not been updated since.

4096 :- The is the number of bytes taken by the file.

infadev infadev :- The first instance of infadev is the owner of the file. This is typically the user who created the file.

The second infadev is the group associated with the file.

3 :- A property of the unix file system is that more than one name can correspond to the same file. This number, called the “reference count”, is the number of names that correspond to this file or directory.

rwxrwxr-x :- These are the permissions on the file or directory. They form three triplets, each a letter or dash. The letter shows the permission is granted and the dash that it is denied.

We can consider the permissions one triple at a time.

rwx :- The first triple identifies the permissions granted to the owner of the file. The user may read from, write to  and execute the file. “Execute” permission means that the owner may run this file as a program.

In the case of a directory, the read permission means that the owner may look to see the names of the files within the directory, the write permission means that owner may add or remove things in the directory and the execute permission means that owner can change directory into it.

rwx :- The second triple indicates the permissions granted to members of the group who are not the owner. 

r-x :- The third triple indicates the permissions granted to any user who is not in the group or the owner of the file.

d :- The first character indicates that this is a directory. If it is a plain file, it will be dash.

42) cd 

The command to change directory. But if the directory is named as Unix Intro then it won’t work

43) Quoting 

In the above case of directory name with space, the quotes tell the shell to treat everything inside them as single word and not split it up on spaces.

cd “Unix Intro”

44) Escaping 

The second approach is to specifically identify the space character as “nothing special, just another character” so the shell doesn’t use it for splitting. We do this by preceding the space with a backslash character, “\”. This is called “escaping” the character.

cd Unix\ Intro

45) File Name completion 

Type the directory name “Unix Intro”, but only get as far as the first letter. Then hit the “Tab” button.

At this point shell determines that there is only one file or directory present that starts with a “U” and automatically extends the file name on the command line, adding any escaping that is necessary.

46) ls -a 

To see the hidden files and directories.

Every unix directory has the two entries “.” and “..” ; They are created automatically and you can’t remove them. The first, “.” refers to the directory itself, so “cd .” has no effect.

The second, “..” refers to the parent directory. Changing directory to “..” takes you up one level in the directory tree.

47) File Paths 

We don’t need to enter a directory to see what’s in it. We don’t need to only change one level of directory tree at a time either.

for eg: $ ls software/informatica

our file paths so far have all started with a component in the current working directory. These are called “relative paths” and refer to files and directories relative to the current working directory.

if a file path starts with a forward slash, “/”, then it is evaluated relative to the  top (the “root”) of the file tree. This is called an “absolute path”.

48) Renaming, creating and deleting file and directories

Renaming and Moving Items: Suppose if we want to rename the file “tall ship.png” to “vikrant.png”. We do this with the mv(“move”) command.

$ mv “tall ship.png” vikrant.png

The move command name is more obvious when used to move file into another directory. We can move files between directories and rename them simultaneously.

Copying Files:- To copy a file, we use the command cp(“copy”) just like we used mv

$ cp vikrant.png viraat.png

It is not possible to copy directory without using an extra option. The option is “-R”(recursive), which means copy the directory and everything in it. 
