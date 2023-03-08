---
title: AWS VPC：使用虚拟私有云保护 Web 应用程序
description: 
published: true
date: 2023-02-01T04:44:20.558Z
tags: 
editor: markdown
dateCreated: 2023-02-01T04:44:16.692Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS VPC: Securing a Web Application with Virtual Private Clouds***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-vpc-securing-a-web-application-with-virtual-private-clouds)
{.links-list}



# AWS VPC：使用虚拟私有云保护 Web 应用程序

AWS VPC 是保护云中 Web 应用程序的重要工具。通过创建 VPC，开发人员可以创建一个虚拟专用网络，将他们的 Web 应用程序与公共互联网隔离开来。这使他们能够控制进出其应用程序的流量，并确保只有授权用户才能访问它。

在本文中，我们将探讨如何使用 AWS VPC 来保护 Web 应用程序。我们将涵盖以下主题：

- 创建专有网络
- 配置安全组
- 配置 NAT 网关
- 测试您的 VPC 配置

## 创建专有网络

使用 VPC 保护 Web 应用程序的第一步是创建 VPC 本身。为此，您可以使用 AWS 管理控制台、AWS 命令行界面 (CLI) 或 AWS 开发工具包。

登录到 AWS 管理控制台后，导航到 VPC 服务。然后，单击左侧导航面板中的“您的 VPC”。

![AWS VPC 控制台](https://i.imgur.com/p0lw9oG.png)

在“您的 VPC”页面上，单击“创建 VPC”按钮。

![创建 VPC](https://i.imgur.com/7Dm7Ncu.png)

在“创建 VPC”页面上，您需要配置以下设置：

- **名称标签**：这是您的 VPC 的名称。它可以是你喜欢的任何东西。
- **CIDR 块**：这是将分配给您的 VPC 的 IP 地址范围。我们建议使用 /16 网络，这将为您提供一系列 IP 地址供您使用。
- **租赁**：默认情况下，您的 VPC 将使用共享租赁创建。这意味着多个 AWS 账户可以使用相同的物理资源。如果您希望您的 VPC 被隔离，您可以选择“专用”租赁选项。这需要额外收费。
- **IPv6 CIDR 块**：您可以选择为您的 VPC 启用 IPv6。这将为您提供一系列可供使用的 IPv6 地址。
- **默认子网**：子网是 VPC 内的 IP 地址范围。默认情况下，AWS 会为您创建一个子网。如果您想创建自己的子网，可以稍后再做。

单击“创建 VPC”按钮以创建您的 VPC。

## 配置安全组

创建 VPC 后，您将需要配置安全组。安全组充当您的 VPC 的防火墙。它们允许您控制进出 VPC 的流量。

要创建安全组，请导航至 VPC 控制台中的“安全组”页面。然后，单击“创建安全组”按钮。

![创建安全组](https://i.imgur.com/vALDK5Y.png)

在“创建安全组”页面上，您需要配置以下设置：

- **安全组名称**：这是您的安全组的名称。它可以是你喜欢的任何东西。
- **描述**：这是对您的安全组的描述。它可以是你喜欢的任何东西。
- **VPC**：选择要与该安全组关联的VPC。

单击“创建安全组”按钮以创建您的安全组。

接下来，您需要将规则添加到您的安全组。为此，请导航至“安全组”页面并选择您要修改的安全组。然后，单击“编辑入站规则”按钮。

![编辑入站规则](https://i.imgur.com/rc9pWxv.png)

在“编辑入站规则”页面上，您需要为以下流量添加规则：

- SSH：这允许来自堡垒主机的端口 22 上的流量。您的堡垒主机是一个 EC2 实例，您将使用它来连接到您的 VPC。
- HTTP：这允许来自任何地方的端口 80 上的流量。
- HTTPS：这允许来自任何地方的端口 443 上的流量。

单击“保存规则”按钮以保存您的更改。

## 配置 NAT 网关

下一步是配置 NAT 网关。 NAT 网关允许您从 VPC 访问互联网。它还允许您通过 VPC 路由互联网流量。

要创建 NAT 网关，请导航至 VPC 控制台中的“NAT 网关”页面。然后，单击“创建 NAT 网关”按钮。

![创建 NAT 网关](https://i.imgur.com/qY0Vn4I.png)

在“创建 NAT 网关”页面上，您需要配置以下设置：

- **NAT 网关名称**：这是您的 NAT 网关的名称。它可以是你喜欢的任何东西。
- **子网**：选择要与此 NAT 网关关联的子网。
- **弹性IP**：选择您要与此NAT 网关关联的弹性IP。

单击“创建 NAT 网关”按钮以创建您的 NAT 网关。

## 测试您的 VPC 配置

创建 VPC 并配置安全组和 NAT 网关后，您可以测试您的配置。为此，您需要在 VPC 中启动一个 EC2 实例。

要启动 EC2 实例，请导航至 EC2 控制台中的“实例”页面。然后，单击“启动实例”按钮。

![启动实例](https://i.imgur.com/9GYNgkO.png)

在“选择 Amazon 系统映像”页面上，选择 Amazon Linux AMI。

![选择亚马逊机器图像](https://i.imgur.com/pH7Ixha.png)

在“选择实例类型”页面上，选择 t2.micro 实例类型。

![选择实例类型](https://i.imgur.com/ukYNTyU.png)

在“配置实例详细信息”页面上，确保配置了以下设置：

- **网络**：选择您要在其中启动此实例的 VPC。
- **子网**：选择您要在其中启动此实例的子网。
- **自动分配公共 IP**：选择“启用”选项。

![配置实例详细信息](https://i.imgur.com/Y0l4U6O.png)

在“添加存储”页面上，您可以保留默认设置并单击“下一步：添加标签”按钮。

在“添加标签”页面上，您可以保留默认设置并单击“下一步：配置安全组”按钮。

在“配置安全组”页面上，选择您之前创建的安全组。然后，单击“查看并启动”按钮。

在“查看实例启动”页面上，单击“启动”按钮。

在“选择现有密钥对或创建新密钥对”页面上，选择要使用的密钥对。然后，单击“启动实例”按钮。

![选择密钥对](https://i.imgur.com/tGcWql8.png)

您的 EC2 实例现在将启动。一旦启动并运行，您可以使用 SSH 连接到它。

![连接到 EC2 实例](https://i.imgur.com/TGiuk72.png)

要测试您的 NAT 网关，您可以使用以下命令 ping 一个网站：

```
ping www.google.com
```

您应该看到类似于以下内容的输出：

```
PING www.google.com (172.217.194.206) 56(84) bytes of data.
64 bytes from muc06s02-in-f14.1e100.net (172.217.194.206): icmp_seq=1 ttl=52 time=52.6 ms
64 bytes from muc06s02-in-f14.1e100.net (172.217.194.206): icmp_seq=2 ttl=52 time=52.5 ms
64 bytes from muc06s02-in-f14.1e100.net (172.217.194.206): icmp_seq=3 ttl=52 time=52.5 ms

--- www.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 52.526/52.561/52.607/0.129 ms
```

要测试您的安全组，您可以尝试从公共互联网访问您的 Web 应用程序。您应该无法访问它。

## 结论

在本文中，我们探索了如何使用 AWS VPC 来保护 Web 应用程序。我们涵盖了以下主题：

- 创建专有网络
- 配置安全组
- 配置 NAT 网关
- 测试您的 VPC 配置

通过执行本文中的步骤，您可以确保您的 Web 应用程序是安全的并且只能由授权用户访问。