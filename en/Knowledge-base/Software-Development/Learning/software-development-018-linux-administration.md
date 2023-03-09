---
title: Software Development 018: Linux Administration
description: 
published: true
date: 2023-03-09T00:32:34.742Z
tags: 
editor: markdown
dateCreated: 2023-03-09T00:32:34.742Z
---

- [소프트웨어 개발 018: Linux 관리***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-018-linux-administration)
{.links-list}



Linux Administration

Linux is an open-source operating system that has gained popularity over the years. It is widely used in servers, supercomputers, and mobile devices. Linux has a reputation for being secure, stable, and flexible. It is also customizable and can be used for a wide range of tasks.

In this post, we will explore Linux administration. We will cover the basics of Linux administration, including user management, file management, and process management. We will also look at some advanced topics, such as network configuration and security.

User Management

User management is an important aspect of Linux administration. Linux allows multiple users to use the same system simultaneously. Each user has a unique username and password. The root user has complete control over the system.

To add a new user, use the useradd command followed by the username. For example:

```
sudo useradd johndoe
```

To set a password for the new user, use the passwd command followed by the username. For example:

```
sudo passwd johndoe
```

To delete a user, use the userdel command followed by the username. For example:

```
sudo userdel johndoe
```

File Management

File management is another important aspect of Linux administration. Linux has a hierarchical file system. The root directory is denoted by / and all other directories are subdirectories of the root directory.

To create a new directory, use the mkdir command followed by the directory name. For example:

```
mkdir mydirectory
```

To create a new file, use the touch command followed by the file name. For example:

```
touch myfile.txt
```

To copy a file, use the cp command followed by the source file and destination file. For example:

```
cp myfile.txt mydirectory/
```

To move a file, use the mv command followed by the source file and destination file. For example:

```
mv myfile.txt mydirectory/
```

Process Management

Process management is an important aspect of Linux administration. Linux allows multiple processes to run simultaneously. Each process has a unique process ID (PID).

To view running processes, use the ps command. For example:

```
ps aux
```

To kill a process, use the kill command followed by the PID. For example:

```
kill 1234
```

Network Configuration

Network configuration is an advanced topic in Linux administration. Linux allows you to configure network interfaces and set up network services.

To view network interfaces, use the ifconfig command. For example:

```
ifconfig
```

To configure a network interface, use the ifconfig command followed by the interface name and the IP address. For example:

```
ifconfig eth0 192.168.1.100 netmask 255.255.255.0
```

To set up a network service, use the systemctl command followed by the service name and the action. For example:

```
systemctl start sshd
```

Security

Security is an important aspect of Linux administration. Linux has built-in security features that allow you to secure your system.

To view system logs, use the journalctl command. For example:

```
journalctl
```

To view failed login attempts, use the lastb command. For example:

```
lastb
```

To install security updates, use the apt-get command followed by the update and upgrade options. For example:

```
sudo apt-get update
sudo apt-get upgrade
```

Additional Information

Linux administration requires a good understanding of the Linux command line. It is important to be familiar with basic Linux commands and their syntax.

Warnings

Be careful when using the root user. The root user has complete control over the system and can cause damage if used improperly.

Dangers

Improperly configuring network services can leave your system vulnerable to attacks. It is important to follow best practices for network security.

External Resources

1. Linux Documentation Project: https://tldp.org/
2. Linux Command: http://linuxcommand.org/
3. Linux Security: https://www.linuxsecurity.com/