---
title: Linux Package Management with apt and yum
description: 
published: true
date: 2023-02-12T09:32:20.578Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:32:18.638Z
---

- [Gestión de paquetes de Linux con apt y yum***Spanish** document is available*](/es/Knowledge-base/Linux/linux-package-management-with-apt-and-yum)
{.links-list}
- [使用 apt 和 yum 进行 Linux 包管理***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-package-management-with-apt-and-yum)
{.links-list}
- [apt 및 yum을 사용한 Linux 패키지 관리***Korean** document is available*](/ko/Knowledge-base/Linux/linux-package-management-with-apt-and-yum)
{.links-list}



# Linux Package Management with apt and yum

Package management is an important part of any Linux distribution. It allows you to install, update, and remove software packages from your system. In this article, we will take a look at two of the most popular package management tools: apt and yum.

## apt

apt (Advanced Package Tool) is the default package manager for Debian and Ubuntu systems. It is a powerful tool that can be used to install, update, and remove software packages from your system. apt is also capable of resolving dependencies, so you don't have to worry about manually installing all the required dependencies for a particular software package.

To install a software package using apt, you can use the following command:

```
sudo apt install {package-name}
```

For example, to install the "vim" text editor, you would use the following command:

```
sudo apt install vim
```

If you want to update all the software packages on your system, you can use the following command:

```
sudo apt update
```

To upgrade all the software packages on your system to their latest versions, you can use the following command:

```
sudo apt upgrade
```

If you want to remove a software package from your system, you can use the following command:

```
sudo apt remove {package-name}
```

For example, to remove the "vim" text editor, you would use the following command:

```
sudo apt remove vim
```

## yum

yum (Yellowdog Updater Modified) is the default package manager for Red Hat and CentOS systems. It is a powerful tool that can be used to install, update, and remove software packages from your system. yum is also capable of resolving dependencies, so you don't have to worry about manually installing all the required dependencies for a particular software package.

To install a software package using yum, you can use the following command:

```
sudo yum install {package-name}
```

For example, to install the "vim" text editor, you would use the following command:

```
sudo yum install vim
```

If you want to update all the software packages on your system, you can use the following command:

```
sudo yum update
```

To upgrade all the software packages on your system to their latest versions, you can use the following command:

```
sudo yum upgrade
```

If you want to remove a software package from your system, you can use the following command:

```
sudo yum remove {package-name}
```

For example, to remove the "vim" text editor, you would use the following command:

```
sudo yum remove vim
```

## Conclusion

In this article, we have looked at two of the most popular package management tools: apt and yum. Both of these tools are powerful and can be used to manage the software packages on your system.