---
title: AWS 弹性 IP：为云资源分配静态 IP 地址
description: 
published: true
date: 2023-02-06T19:17:38.032Z
tags: 
editor: markdown
dateCreated: 2023-02-06T19:17:36.378Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS Elastic IPs: Allocating Static IP Addresses for Cloud Resources***English** document is available*](/en/Knowledge-base/Cloud/aws-elastic-ips-allocating-static-ip-addresses-for-cloud-resources)
{.links-list}


# AWS 弹性 IP：为云资源分配静态 IP 地址

弹性IP地址是为动态云计算设计的静态IP地址。弹性 IP 地址与您的 AWS 账户相关联。使用弹性 IP 地址，您可以通过将地址快速重新映射到您账户中的另一个实例来掩盖实例或软件的故障。

弹性 IP 地址是可以分配给实例或网络接口的公共 IP 地址。如果您将弹性 IP 地址与已有公网 IP 地址的实例相关联，则实例的原始公网 IP 地址将替换为弹性 IP 地址。如果将弹性 IP 地址与网络接口相关联，则该 IP 地址将与网络接口的主要私有 IP 地址相关联。

您可以在使用 Amazon EC2 控制台创建实例时分配新的弹性 IP 地址。您还可以从现有的弹性 IP 地址池中分配一个新的弹性 IP 地址。您可以随时将弹性 IP 地址与实例或网络接口相关联。

如果您取消弹性 IP 地址与实例的关联，则会从 Amazon EC2 公共 IP 地址池中为该实例分配一个新的公共 IP 地址。如果取消弹性IP地址与网络接口的关联，则网络接口的主私有IP地址将从弹性IP地址重新分配到子网IP地址池中的另一个私有IP地址。

## 分配弹性 IP 地址

使用 Amazon EC2 控制台分配弹性 IP 地址

1. 在 https://console.aws.amazon.com/ec2/ 打开 Amazon EC2 控制台。

2. 在导航窗格中，选择 **弹性 IPs**。

3. 选择**分配新地址**。

4. 选择**分配**。

5. 选择**关闭**。

您的弹性 IP 地址现已分配并准备好与实例或网络接口相关联。

## 将弹性 IP 地址与实例关联

使用 Amazon EC2 控制台将弹性 IP 地址与实例相关联

1. 在 https://console.aws.amazon.com/ec2/ 打开 Amazon EC2 控制台。

2. 从实例列表中选择实例。

3. 选择 **Actions**、**Networking**、**Change Elastic IP Address**、**Associate Elastic IP Address**。

4. 从列表中选择弹性 IP 地址，然后选择 **Associate**。

您的实例现在与弹性 IP 地址相关联。

## 将弹性 IP 地址与网络接口相关联

使用 Amazon EC2 控制台将弹性 IP 地址与网络接口相关联

1. 在 https://console.aws.amazon.com/ec2/ 打开 Amazon EC2 控制台。

2. 在导航窗格中，选择 **网络接口**。

3. 选择网络接口，然后选择**Action**、**Networking**、**Change Elastic IP Address**、**Associate Elastic IP Address**。

4. 从列表中选择弹性 IP 地址，然后选择 **Associate**。

您的网络接口现在与弹性 IP 地址相关联。

## 取消关联弹性 IP 地址

使用 Amazon EC2 控制台取消弹性 IP 地址与实例或网络接口的关联

1. 在 https://console.aws.amazon.com/ec2/ 打开 Amazon EC2 控制台。

2. 在导航窗格中，选择 **弹性 IPs**。

3. 选中要取消关联的弹性 IP 地址旁边的复选框。

4. 选择 **Actions**、**Networking**、**Change Elastic IP Address**、**Disassociate Elastic IP Address**。

5. 当提示确认时，选择 **Yes, Disassociate**。

弹性 IP 地址现在与实例或网络接口解除关联。

## 释放弹性 IP 地址

您可以在不再需要时释放弹性 IP 地址。使用 Amazon EC2 控制台释放弹性 IP 地址

1. 在 https://console.aws.amazon.com/ec2/ 打开 Amazon EC2 控制台。

2. 在导航窗格中，选择 **弹性 IPs**。

3. 选中您要释放的弹性IP地址旁边的复选框。

4. 选择 **Actions**、**Networking**、**Change Elastic IP Address**、**Release Elastic IP Address**。

5. 当提示确认时，选择 **Yes, Release**。

弹性 IP 地址现已释放，不再与您的 AWS 账户相关联。

## 附加信息

有关弹性 IP 地址的更多信息，请参阅以下内容：

- Linux 实例的 Amazon EC2 用户指南中的弹性 IP 地址
- 适用于 Windows 实例的 Amazon EC2 用户指南中的弹性 IP 地址

## 外部资源

- Amazon EC2：弹性 IP 地址 (EIP)
- AWS IP地址规划
- 如何使用 AWS 弹性 IP