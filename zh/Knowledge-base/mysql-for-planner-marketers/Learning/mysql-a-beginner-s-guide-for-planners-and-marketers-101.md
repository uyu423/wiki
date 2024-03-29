---
title: MySQL 规划人员和营销人员初学者指南：101
description: 
published: true
date: 2023-02-06T16:34:09.381Z
tags: 
editor: markdown
dateCreated: 2023-02-06T16:34:07.575Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [MySQL A Beginner's Guide for Planners and Marketers: 101***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-a-beginner-s-guide-for-planners-and-marketers-101)
{.links-list}


MySQL 是一个强大的数据库管理系统，Web 应用程序使用它来存储数据。它是当今最流行的数据库系统之一。

MySQL 是一种关系数据库管理系统 (RDBMS)。这意味着它将数据存储在彼此相关的表中。例如，客户数据表可能与订单数据表相关。

MySQL 是一个免费的开源软件。这意味着它可供任何人使用和修改。

MySQL 是 Web 应用程序的流行选择，因为它快速、可靠且易于使用。

在本指南中，我们将学习 MySQL 的基础知识。我们将涵盖以下主题：

- 安装 MySQL
- 创建数据库
- 创建表格
- 插入数据
- 查询数据
- 备份还原

## 安装 MySQL

MySQL 可以安装在 Windows、macOS 和 Linux 上。它也可以安装在运行其他操作系统（例如 FreeBSD）的服务器上。

在 Windows 上安装 MySQL 的最简单方法是使用 MySQL 安装程序。这将安装我们需要的所有组件，包括 MySQL Server、MySQL Workbench 和 MySQL Notifier。

从 MySQL 网站下载 MySQL 安装程序：

https://dev.mysql.com/downloads/installer/

运行安装程序并按照提示进行操作。出现提示时，选择以下选项：

- 安装 MySQL 服务器
- 立即配置 MySQL 服务器

配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，为 MySQL root 用户选择一个密码。这是对所有 MySQL 数据库具有完全访问权限的用户。

在下一页上，选择以下选项：

- 安装为 Windows 服务
- 在 Windows PATH 中包含 Bin 目录

在下一页上，选择以下选项：

- 端口号：3306
- 启用 TCP/IP 网络
- 启用严格模式

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择以下选项：

安装为 Windows 服务：是
- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 端口号：3306
启用 TCP/IP 网络：是
启用严格模式：是

在下一页上，选择以下选项：

- 默认字符集：utf8
- 安装 MySQL 测试套件：是

在下一页上，选择以下选项：

- MySQL 通知程序：不需要
- MySQL Workbench：不需要

在下一页上，选择以下选项：

- 创建匿名帐户：否
- 启用严格的密码验证：否

在下一页上，选择以下选项：

- 将 MySQL 服务器作为 Windows 服务运行：是
- 自动启动 MySQL 服务器：是

在下一页上，选择以下选项：

- 在 Windows PATH 中包含 Bin 目录：是

在下一页上，选择以下选项：

- 立即配置 MySQL 服务器：是

MySQL 服务器配置向导将启动。在第一页上，选择以下选项：

- 服务器类型：开发机
- 数据库使用：多功能数据库
- 事务数据库支持：InnoDB
- 非事务性数据库支持：MyISAM

在下一页上，选择