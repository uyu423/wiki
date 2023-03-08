---
title: Remote Desktop Protocol
description: 
published: true
date: 2023-02-17T18:06:22.460Z
tags: 
editor: markdown
dateCreated: 2023-01-30T14:54:36.207Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Remote Desktop Protocol***English** version of this document is available*](/en/Knowledge-base/Dictionary/remote-desktop-protocol)
{.links-list}


# 概述
远程桌面协议（Remote Desktop Protocol，RDP）是微软开发的一种协议，它为用户提供图形界面，通过网络连接到另一台计算机。它允许用户访问远程计算机上的资源和数据，就像他们坐在它前面一样。 RDP 通常用于远程系统管理和故障排除，以及访问远程计算机上的应用程序或文件。

# 历史
RDP最早由微软于1995年开发，最初包含在Windows NT 4.0操作系统中。该协议后来被包含在其他版本的 Windows 中，包括 Windows XP、Windows Vista、Windows 7 和 Windows 8。2014 年，Microsoft 发布了 RDP 的更新版本，称为远程桌面协议 8.1，它增加了对新功能的支持，例如RemoteFX 和改进的性能。

# 描述
RDP 基于客户端-服务器模型，其中远程桌面客户端建立到远程桌面服务器的连接。客户端向服务器发送命令，服务器执行命令，并将结果发送回客户端。客户端和服务器使用专有协议进行通信，该协议使用传输层安全性 (TLS) 加密。

客户端和服务器使用远程会话协议（例如远程帧缓冲区 (RFB)）来交换图形数据和控制信息。客户端可以在自己的屏幕上显示远程桌面，允许用户像在本地一样与远程计算机交互。客户端和服务器还可以交换音频和打印机数据。

# 题外话
RDP 旨在提供对计算机资源的远程访问，包括应用程序、文件和网络资源。它通常用于系统管理和故障排除，以及访问远程计算机上的应用程序或文件。此外，RDP 可用于远程协作，允许多个用户同时访问一台计算机。

# 相关链接
- [什么是远程桌面协议 (RDP)？*Microsoft*](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-protocol)
- [了解远程桌面协议*TechTarget*](https://searchvirtualdesktop.techtarget.com/definition/Remote-Desktop-Protocol-RDP)
- [远程桌面协议 (RDP)*维基百科*](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol)
{.links-list}