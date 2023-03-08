---
title: AWS Lightsail：使用完全托管的 PaaS 启动简单的网站和应用程序
description: 
published: true
date: 2023-02-06T11:56:00.308Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:55:58.664Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS Lightsail: Launching Simple Websites and Applications with a Fully Managed PaaS***English** document is available*](/en/Knowledge-base/Cloud/aws-lightsail-launching-simple-websites-and-applications-with-a-fully-managed-paas)
{.links-list}


# AWS Lightsail：使用完全托管的 PaaS 启动简单的网站和应用程序

AWS Lightsail 是一个完全托管的平台即服务 (PaaS)，可以轻松启动简单的网站和应用程序。 Lightsail 包含启动项目所需的一切，包括虚拟专用服务器、托管数据库、DNS 管理和静态 IP 地址。

Lightsail 是启动简单网站和应用程序的绝佳选择，因为它易于使用，而且您只需为使用的资源付费。没有前期成本或长期合同。您可以在几分钟内创建一个 Lightsail 实例，并且可以随着项目的增长扩展资源。

## 开始使用 Lightsail

要开始使用 Lightsail，您首先需要创建一个帐户并选择一个区域。您可以在 https://lightsail.aws.amazon.com/ 创建一个帐户。

创建帐户后，您可以创建 Lightsail 实例。为此，请单击“创建实例”按钮并选择您的实例类型。 Lightsail 提供多种实例类型，包括 Linux 和 Windows 虚拟专用服务器、容器和静态 IP 地址。

选择实例类型后，您可以选择实例计划。 Lightsail 提供多种计划，包括月度和小时计划。

选择实例计划后，您可以为实例选择操作系统、应用程序和其他资源。 Lightsail 提供各种流行的操作系统，包括 Amazon Linux、Ubuntu 和 Windows Server。

您还可以为您的实例选择应用程序和其他资源，例如 WordPress、Drupal、Joomla! 和 Magento。

为您的实例选择操作系统、应用程序和其他资源后，您可以为您的实例选择一个名称，然后单击“创建实例”按钮。

现在将创建您的 Lightsail 实例，您将能够通过 Lightsail 控制台访问它。

## 连接到您的 Lightsail 实例

要连接到您的 Lightsail 实例，您首先需要下载 Lightsail 客户端。 Lightsail 客户端是一个命令行界面 (CLI)，您可以使用它来管理您的 Lightsail 资源。

您可以从 Lightsail 控制台下载 Lightsail 客户端。为此，请单击“帐户”菜单并选择“下载客户端”。

下载 Lightsail 客户端后，您可以使用以下命令连接到您的 Lightsail 实例：

```
lightsail-client connect --instance-name my-instance
```

将“我的实例”替换为您的 Lightsail 实例的名称。

现在系统将提示您输入您的 Lightsail 用户名和密码。输入凭据后，您将连接到 Lightsail 实例。

## 管理您的 Lightsail 实例

连接到 Lightsail 实例后，您可以使用 Lightsail 客户端来管理您的实例。

要查看所有可用命令的列表，您可以使用“帮助”命令：

```
lightsail-client help
```

要查看有关特定命令的信息，您可以使用“help”命令，后跟命令名称。例如，要查看“connect”命令的信息，可以使用以下命令：

```
lightsail-client help connect
```

要查看您账户中所有 Lightsail 实例的列表，您可以使用“list-instances”命令：

```
lightsail-client list-instances
```

要查看有关特定 Lightsail 实例的信息，您可以使用“describe-instance”命令，后跟实例名称。例如，要查看有关“my-instance”Lightsail 实例的信息，您可以使用以下命令：

```
lightsail-client describe-instance --instance-name my-instance
```

要停止 Lightsail 实例，您可以使用“stop-instance”命令，后跟实例名称。例如，要停止“my-instance”Lightsail 实例，您可以使用以下命令：

```
lightsail-client stop-instance --instance-name my-instance
```

要启动 Lightsail 实例，您可以使用“start-instance”命令，后跟实例名称。例如，要启动“my-instance”Lightsail 实例，您可以使用以下命令：

```
lightsail-client start-instance --instance-name my-instance
```

要删除 Lightsail 实例，您可以使用“delete-instance”命令，后跟实例名称。例如，要删除“my-instance”Lightsail 实例，您可以使用以下命令：

```
lightsail-client delete-instance --instance-name my-instance
```

## 创建 Lightsail 快照

Lightsail 快照是 Lightsail 实例的时间点备份。您可以使用快照创建新的 Lightsail 实例或恢复现有的 Lightsail 实例。

要创建 Lightsail 实例的快照，您可以使用“create-snapshot”命令，后跟实例名称。例如，要创建“my-instance”Lightsail 实例的快照，您可以使用以下命令：

```
lightsail-client create-snapshot --instance-name my-instance
```

要查看您帐户中所有快照的列表，您可以使用“list-snapshots”命令：

```
lightsail-client list-snapshots
```

要查看有关特定快照的信息，您可以使用“describe-snapshot”命令，后跟快照名称。例如查看“my-snapshot”快照的信息，可以使用如下命令：

```
lightsail-client describe-snapshot --snapshot-name my-snapshot
```

要删除快照，您可以使用“delete-snapshot”命令，后跟快照名称。例如删除“my-snapshot”快照，可以使用如下命令：

```
lightsail-client delete-snapshot --snapshot-name my-snapshot
```

## 从快照创建 Lightsail 实例

要从快照创建 Lightsail 实例，您可以使用“create-instance-from-snapshot”命令，后跟快照名称。例如，要从“my-snapshot”快照创建 Lightsail 实例，您可以使用以下命令：

```
lightsail-client create-instance-from-snapshot --snapshot-name my-snapshot
```

## 结论

在本文中，我们了解了如何使用 AWS Lightsail 启动简单的网站和应用程序。 Lightsail 是启动简单网站和应用程序的绝佳选择，因为它易于使用，而且您只需为使用的资源付费。

如果您正在寻找一个完全托管的 PaaS 来启动您的下一个项目，那么 Lightsail 是一个不错的选择。