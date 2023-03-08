---
title: File Permissions and Ownership in Linux
description: 
published: true
date: 2023-02-11T08:32:29.790Z
tags: 
editor: markdown
dateCreated: 2023-02-11T08:32:23.266Z
---

- [Permisos de archivo y propiedad en Linux***Spanish** document is available*](/es/Knowledge-base/Linux/file-permissions-and-ownership-in-linux)
{.links-list}
- [Linux 中的文件权限和所有权***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/file-permissions-and-ownership-in-linux)
{.links-list}
- [Linux의 파일 권한 및 소유권***Korean** document is available*](/ko/Knowledge-base/Linux/file-permissions-and-ownership-in-linux)
{.links-list}


# File Permissions and Ownership in Linux

In any Linux system, file permissions and ownership are very important in order to ensure that files are accessed and used in the way that you want. In this article, we will take a look at what file permissions and ownership are, how they work, and some common scenarios where you might need to use them.

## What are file permissions and ownership?

File permissions are settings that determine who is able to read, write, or execute a particular file. File ownership determines who has control over a file and can change its permissions.

In Linux, every file has two sets of permissions: 
- The permissions for the file owner 
- The permissions for everyone else 

You can view the permissions for a file using the `ls -l` command. This will give output that looks something like this:

```
-rw-r--r-- 1 root root 696 Apr 3 12:34 somefile
```

The first column shows the permissions for the owner, the second column shows the permissions for everyone else, and the third and fourth columns show the file owner and group, respectively.

The permissions are represented by a series of letters: `r`, `w`, and `x`. 
- `r` stands for read and means that the file can be read 
- `w` stands for write and means that the file can be written to 
- `x` stands for execute and means that the file can be executed as a program

If a permission is not set, it is represented by a `-`. For example, the `ls -l` output above shows that the owner has read and write permissions but not execute permissions, while everyone else has only read permissions.

## How do file permissions and ownership work?

The file owner is the user who created the file. The file group is a collection of users who have access to the file. By default, the file group is usually the same as the file owner, but it can be changed.

Each file also has a set of permissions that determine who can read, write, or execute it. These permissions can be changed by the file owner or by a user with root privileges.

To change the file owner, you can use the `chown` command. For example, to change the owner of a file called `somefile` to the user `jane`, you would use the command `chown jane somefile`.

To change the file group, you can use the `chgrp` command. For example, to change the group of a file called `somefile` to the group `users`, you would use the command `chgrp users somefile`.

To change the file permissions, you can use the `chmod` command. There are two ways to use this command: 
- With numbers 
- With letters 

The numbers represent the permissions for the owner, the group, and everyone else, respectively. The letters represent the same thing but are more user-friendly. 

For example, to give the owner read, write, and execute permissions, the group read and execute permissions, and everyone else read permissions, you would use the command `chmod 751 somefile`. 

You can also use letters to represent the permissions. To give the owner read, write, and execute permissions, the group read and execute permissions, and everyone else read permissions, you would use the command `chmod u=rwx,g=rx,o=r somefile`.

## Scenarios where you might need to use file permissions and ownership

There are a few common scenarios where you might need to use file permissions and ownership: 

### When you want to allow other users to access your files

If you want to allow other users on the same system to access your files, you will need to set the appropriate permissions. For example, if you want to allow other users to read and write to a file called `somefile`, you would use the command `chmod 664 somefile`.

### When you want to prevent other users from accessing your files

If you want to prevent other users on the same system from accessing your files, you will need to set the appropriate permissions. For example, if you want to prevent other users from reading a file called `somefile`, you would use the command `chmod 600 somefile`.

### When you want to allow users on other systems to access your files

If you want to allow users on other systems to access your files, you will need to set the appropriate permissions. For example, if you want to allow users on other systems to read and write to a file called `somefile`, you would use the command `chmod 666 somefile`.

### When you want to prevent users on other systems from accessing your files

If you want to prevent users on other systems from accessing your files, you will need to set the appropriate permissions. For example, if you want to prevent users on other systems from reading a file called `somefile`, you would use the command `chmod 400 somefile`.

## Conclusion

In this article, we have taken a look at what file permissions and ownership are, how they work, and some common scenarios where you might need to use them. File permissions and ownership are important in any Linux system in order to ensure that files are accessed and used in the way that you want.