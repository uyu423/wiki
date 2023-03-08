---
title: Linux 系统管理
description: 
published: true
date: 2023-02-11T11:32:22.314Z
tags: 
editor: markdown
dateCreated: 2023-02-11T11:32:20.716Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [System Administration with Linux***English** document is available*](/en/Knowledge-base/Linux/system-administration-with-linux)
{.links-list}


# Linux 系统管理

系统管理是管理计算机系统的过程。通常，系统管理包括安装软件、配置硬件和管理用户帐户等任务。

系统管理可以由具有适当权限的用户执行，例如根用户。然而，在实践中，系统管理通常由专门的管理员团队执行。

## 安装软件

系统管理员最常见的任务之一是安装软件。这可以使用诸如 apt 之类的包管理器来完成。

Apt 是一个命令行工具，可用于安装、更新和删除软件。它是 Debian 和 Ubuntu 的默认包管理器。

要使用 apt 安装软件包，管理员可以使用以下命令：

```
sudo apt install {package_name}
```

## 配置硬件

系统管理员的另一项常见任务是配置硬件。这可以使用硬件管理工具 hw-config 来完成。

hw-config 是一个命令行工具，可用于配置硬件设备。它可用于配置声卡、网卡和打印机队列等设备。

要使用 hw-config 配置设备，管理员可以使用以下命令：

```
sudo hw-config {device_name}
```

## 管理用户帐户

系统管理员的另一项常见任务是管理用户帐户。这可以使用用户管理工具 usermod 来完成。

Usermod 是一个命令行工具，可用于添加、修改和删除用户帐户。它还可用于更改用户帐户的密码。

要使用 usermod 添加用户，管理员可以使用以下命令：

```
sudo usermod -a -G {group_name} {username}
```

要使用 usermod 更改用户的密码，管理员可以使用以下命令：

```
sudo usermod -p {new_password} {username}
```

## 外部资源

有关系统管理的更多信息，请参阅以下资源：

- [系统管理指南](https://www.tldp.org/LDP/sag/html/)
- [Debian 管理指南](https://debian-handbook.info/browse/stable/)
- [Ubuntu 服务器指南](https://help.ubuntu.com/lts/serverguide/index.html)