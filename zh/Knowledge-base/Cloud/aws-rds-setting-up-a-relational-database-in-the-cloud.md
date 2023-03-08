---
title: AWS RDS：在云中设置关系数据库
description: 
published: true
date: 2023-01-31T02:25:35.932Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:25:34.344Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [AWS RDS: Setting Up a Relational Database in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-rds-setting-up-a-relational-database-in-the-cloud)
{.links-list}



# AWS RDS：在云中设置关系数据库

AWS Relational Database Service (RDS) 是一种托管数据库服务，支持多种数据库引擎，包括 MySQL、MariaDB、Oracle、Microsoft SQL Server 和 PostgreSQL。 RDS 使在云中设置、操作和扩展关系数据库变得容易。

在本文中，我们将引导您完成在 AWS RDS 上设置 MySQL 数据库的过程。我们还将提供一些关于如何保护您的数据库的提示，以及如何解决您可能遇到的常见问题。

##在 AWS RDS 上创建 MySQL 数据库

在 AWS RDS 上创建 MySQL 数据库之前，您需要创建一个 Amazon Web Services (AWS) 帐户。如果您还没有 AWS 账户，可以在 http://aws.amazon.com/ 创建一个。

创建 AWS 帐户后，您可以通过转到 Amazon RDS 主页并单击“启动数据库实例”按钮来启动 RDS 控制台。

在下一页上，您需要选择“MySQL”引擎，然后选择“标准创建”选项。

![标准创建选项](https://i.imgur.com/1ly7YUV.png)

在下一页上，您需要为数据库实例提供名称，以及用于连接数据库的用户名和密码。

![数据库实例](https://i.imgur.com/LxhmJN7.png)

您还需要选择数据库实例的大小，以及它所在的区域。对于此示例，我们将使用“db.t2.micro”实例类型和“美国东部（弗吉尼亚北部）”区域。

![数据库实例类型](https://i.imgur.com/rVg0U6Z.png)

在下一页上，您需要选择是否要为数据库实例启用账单提醒和标记。对于此示例，我们将启用这两个选项。

![数据库实例标记](https://i.imgur.com/eiU3Qnl.png)

在下一页上，您需要指定数据库实例的设置。对于此示例，我们将使用默认设置。

![数据库实例设置](https://i.imgur.com/xk0tU8S.png)

在下一页上，您需要检查数据库实例的设置，然后单击“启动数据库实例”按钮。

![数据库实例回顾](https://i.imgur.com/TGiukmn.png)

现在将创建您的数据库实例，几分钟后即可使用。

## 连接到您的 MySQL 数据库

创建数据库实例后，您可以使用任何与 MySQL 兼容的客户端（例如 MySQL Workbench）连接到它。要连接到您的数据库实例，您需要提供以下信息：

- **端点**：这是您的数据库实例的 URL。您可以在 RDS 控制台的“连接性和安全性”部分找到此信息。

- **端口**：MySQL 的默认端口是 3306。

- **用户名**：您在启动数据库实例时指定的用户名。

- **密码**：您在启动数据库实例时指定的密码。

![数据库实例连接](https://i.imgur.com/CnjNJTV.png)

您现在应该能够连接到您的数据库并运行 SQL 查询。

## 保护你的 MySQL 数据库

保护 MySQL 数据库以防止未经授权的访问非常重要。 AWS RDS 通过提供可用于控制对数据库实例的访问的防火墙，可以轻松保护您的数据库。

要向防火墙添加新规则，请转到 RDS 控制台的“安全组”部分，然后单击“编辑入站规则”按钮。

![数据库实例安全组](https://i.imgur.com/Jz4U3vN.png)

在下一页上，您需要指定规则的类型，以及规则的源和目标。对于此示例，我们将允许从任何来源 (0.0.0.0/0) 访问我们的数据库实例。

![数据库实例安全组规则](https://i.imgur.com/taY0TGi.png)

您现在可以单击“保存规则”按钮来保存您的更改。

## 排除 MySQL 数据库问题

在 AWS RDS 上设置或使用 MySQL 数据库时，您可能会遇到一些常见问题。

- **连接问题**：如果您在连接到数据库时遇到问题，请确保您使用的是正确的端点、端口和凭据。您也可以尝试暂时禁用防火墙，看看这是否是问题的原因。

- **性能低下**：如果您遇到性能低下的问题，请确保您使用的实例类型适合您的工作负载。您可能还需要增加数据库实例的大小。

- **1040 错误**：如果您收到“1040 - 连接太多”错误，则需要增加数据库实例的大小。