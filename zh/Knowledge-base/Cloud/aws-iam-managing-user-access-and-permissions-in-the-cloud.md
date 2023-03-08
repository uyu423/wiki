---
title: AWS IAM：管理云中的用户访问和权限
description: 
published: true
date: 2023-01-31T08:43:44.507Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:43:42.836Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS IAM: Managing User Access and Permissions in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-iam-managing-user-access-and-permissions-in-the-cloud)
{.links-list}



# AWS IAM：管理云中的用户访问和权限

负责管理云中用户访问和权限的开发人员和运营商需要了解可供他们使用的不同工具和服务。本文概述了 AWS Identity and Access Management (IAM) 服务以及如何使用它来管理云中的用户访问和权限。

# # 什么是 AWS IAM？

AWS Identity and Access Management (IAM) 是一种 Web 服务，可帮助您安全地控制对 AWS 资源的访问。 IAM 是您的 AWS 账户的一项功能，它独立于资源本身。 IAM 允许您创建和管理用户和组，并使用权限来允许和拒绝他们对 AWS 资源的访问。

IAM 是一种通用服务，不特定于任何一个区域。它在全球所有 AWS 区域可用。

# # AWS IAM 是如何工作的？

AWS IAM 由以下组件组成：

- **用户**：IAM 用户是用于访问 AWS 资源的 AWS 账户。 IAM 用户不同于用于访问 AWS 管理控制台的 AWS 账户。默认情况下，IAM 用户没有任何权限。您必须明确向 IAM 用户授予权限。

- **组**：IAM 组是 IAM 用户的集合。组是一次管理多个 IAM 用户的一种方式。 IAM 组可用于为多个用户指定权限，这在您拥有大量用户或经常需要更改大量用户的权限时非常有用。

- **策略**：IAM 策略是指定允许 IAM 用户或组对哪些 AWS 资源执行哪些操作的文档。 IAM 策略是用 JSON 编写的。

- **角色**：IAM 角色是一种将对 AWS 资源的访问权限委托给您信任的实体的方式。角色用于向您不信任您的 AWS 凭证的 IAM 用户或组授予权限。角色还可用于向需要访问您的资源的 AWS 服务授予权限，例如 Amazon S3 或 Amazon DynamoDB。

IAM 是一项通用服务，这意味着它不特定于任何一个地区。它在全球所有 AWS 区域可用。

# # 创建 IAM 用户

IAM 用户是用于访问 AWS 资源的 AWS 账户。 IAM 用户不同于用于访问 AWS 管理控制台的 AWS 账户。默认情况下，IAM 用户没有任何权限。您必须明确向 IAM 用户授予权限。

要创建 IAM 用户，您必须先创建一个 IAM 组。 IAM 组是 IAM 用户的集合。 IAM 组可用于为多个用户指定权限，这在您拥有大量用户或经常需要更改大量用户的权限时非常有用。

创建 IAM 组后，您可以将 IAM 用户添加到该组。要将 IAM 用户添加到组，您必须具有 iam:AddUserToGroup 权限。

# # 将策略附加到 IAM 用户

策略是指定允许 IAM 用户或组对哪些 AWS 资源执行哪些操作的文档。 IAM 策略是用 JSON 编写的。

您可以通过两种方式将策略附加到 IAM 用户：

- 您可以在用户数据中嵌入策略。
- 您可以创建一个策略，然后将其附加到用户。

策略可以附加到多个用户和组。

# # 创建 IAM 角色

IAM 角色是一种将对 AWS 资源的访问权限委托给您信任的实体的方法。角色用于向您不信任您的 AWS 凭证的 IAM 用户或组授予权限。角色还可用于向需要访问您的资源的 AWS 服务授予权限，例如 Amazon S3 或 Amazon DynamoDB。

要创建 IAM 角色，您必须先创建 IAM 策略。 IAM 策略是指定允许 IAM 用户或组对哪些 AWS 资源执行哪些操作的文档。 IAM 策略是用 JSON 编写的。

创建 IAM 策略后，您可以创建 IAM 角色并将策略附加到该角色。

可以从 IAM 用户和组附加和分离角色。

# # 删除 IAM 用户

IAM 用户可以随时删除。删除 IAM 用户时，该用户的所有权限也将被删除。删除 IAM 用户不会删除该用户有权访问的 AWS 资源。

要删除 IAM 用户，您必须具有 iam:DeleteUser 权限。

## 概括

AWS Identity and Access Management (IAM) 是一种 Web 服务，可帮助您安全地控制对 AWS 资源的访问。 IAM 是您的 AWS 账户的一项功能，它独立于资源本身。 IAM 允许您创建和管理用户和组，并使用权限来允许和拒绝他们对 AWS 资源的访问。

IAM 是一种通用服务，不特定于任何一个区域。它在全球所有 AWS 区域可用。

IAM 用户是用于访问 AWS 资源的 AWS 账户。 IAM 用户不同于用于访问 AWS 管理控制台的 AWS 账户。默认情况下，IAM 用户没有任何权限。您必须明确向 IAM 用户授予权限。

IAM 组是 IAM 用户的集合。 IAM 组可用于为多个用户指定权限，这在您拥有大量用户或经常需要更改大量用户的权限时非常有用。

策略是指定允许 IAM 用户或组对哪些 AWS 资源执行哪些操作的文档。 IAM 策略是用 JSON 编写的。

IAM 角色是一种将对 AWS 资源的访问权限委托给您信任的实体的方法。角色用于向您不信任您的 AWS 凭证的 IAM 用户或组授予权限。角色还可用于向需要访问您的资源的 AWS 服务授予权限，例如 Amazon S3 或 Amazon DynamoDB。

IAM 是一项通用服务，这意味着它不特定于任何一个地区。它在全球所有 AWS 区域可用。