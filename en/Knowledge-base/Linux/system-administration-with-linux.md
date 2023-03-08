---
title: System Administration with Linux
description: 
published: true
date: 2023-02-11T11:32:27.427Z
tags: 
editor: markdown
dateCreated: 2023-02-11T11:32:20.722Z
---

- [Administración de sistemas con Linux***Spanish** document is available*](/es/Knowledge-base/Linux/system-administration-with-linux)
{.links-list}
- [Linux 系统管理***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/system-administration-with-linux)
{.links-list}
- [Linux를 사용한 시스템 관리***Korean** document is available*](/ko/Knowledge-base/Linux/system-administration-with-linux)
{.links-list}


# System Administration with Linux

System administration is the process of managing a computer system. In general, system administration includes tasks such as installing software, configuring hardware, and managing user accounts.

System administration can be performed by a user with appropriate privileges, such as a root user. However, in practice, system administration is often performed by a dedicated team of administrators.

## Installing Software

One of the most common tasks for a system administrator is to install software. This can be done using a package manager such as apt.

Apt is a command-line tool that can be used to install, update, and remove software. It is the default package manager for Debian and Ubuntu.

To install a package using apt, the administrator can use the following command:

```
sudo apt install {package_name}
```

## Configuring Hardware

Another common task for a system administrator is to configure hardware. This can be done using the hardware management tool, hw-config.

Hw-config is a command-line tool that can be used to configure hardware devices. It can be used to configure devices such as sound cards, network cards, and printer queues.

To configure a device using hw-config, the administrator can use the following command:

```
sudo hw-config {device_name}
```

## Managing User Accounts

Another common task for a system administrator is to manage user accounts. This can be done using the user management tool, usermod.

Usermod is a command-line tool that can be used to add, modify, and delete user accounts. It can also be used to change the password for a user account.

To add a user using usermod, the administrator can use the following command:

```
sudo usermod -a -G {group_name} {username}
```

To change the password for a user using usermod, the administrator can use the following command:

```
sudo usermod -p {new_password} {username}
```

## External Resources

For more information on system administration, see the following resources:

- [System Administration Guide](https://www.tldp.org/LDP/sag/html/)
- [Debian Administration Guide](https://debian-handbook.info/browse/stable/)
- [Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/index.html)