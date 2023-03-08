---
title: 为后端应用程序实现身份验证和授权
description: 
published: true
date: 2023-02-09T02:17:46.832Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:17:45.264Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Implementing Authentication and Authorization for Backend Applications***English** document is available*](/en/Knowledge-base/Backend/implementing-authentication-and-authorization-for-backend-applications)
{.links-list}

      
# 实现后端应用的认证和授权

您已经构建了一个很棒的后端应用程序，现在是时候添加身份验证和授权了。但你从哪儿开始呢？

后端应用程序的身份验证和授权有多种实现方式。在本文中，我们将概述最常用的方法，并为每种方法提供一些实用技巧。

## 验证

身份验证是验证用户是否与他们声称的身份相符的过程。最常见的方法是使用用户名和密码。

当用户尝试登录您的应用程序时，您需要检查他们的用户名和密码是否正确。这可以通过用户数据库或外部服务（如 Active Directory）来完成。

如果用户名和密码正确，您将需要生成用户可用于访问应用程序的令牌。此令牌对用户来说应该是唯一的，并且应该安全地存储。

生成令牌的一种方法是使用 JSON Web 令牌 (JWT)。 JWT 包含有关用户的信息并使用秘密进行签名。这意味着您可以确定令牌未被篡改。

要使用 JWT，您首先需要创建一个秘密。这可以使用像 openssl 这样的工具来完成：

```
 openssl rand -base64 32
```

一旦你有了秘密，你就可以创建一个 JWT：

```
jwt.sign({ user_id: 1 }, secret, { expiresIn: '1h' })
```

这将生成一个在一小时后过期的令牌。当用户向您的应用程序发出请求时，您可以使用此令牌对用户进行身份验证。

要验证令牌，您将需要用于创建它的秘密。然后您可以使用它来验证令牌：

```
jwt.verify(token, secret)
```

如果令牌有效，您可以确定用户就是他们声称的那个人。

另一种生成令牌的方法是使用像 Auth0 这样的工具。 Auth0 是一种将身份验证和授权作为服务提供的服务。这意味着您不必担心构建自己的身份验证和授权系统。

使用 Auth0，您可以通过使用用户名和密码登录用户来创建令牌。然后 Auth0 将为用户生成一个令牌。当用户向您的应用程序发出请求时，此令牌可用于对用户进行身份验证。

要验证令牌，您需要使用 Auth0 服务。然后，您可以使用 Auth0 服务来验证令牌并获取有关用户的信息：

```
auth0.verifyToken(token, function(err, user) {
  if (err) {
    // the token is invalid
  } else {
    // the token is valid
    // you can use the user object to get information about the user
  }
})
```

 Auth0 还提供了一种为 API 调用生成令牌的方法。这意味着您可以使用 Auth0 对您的 API 的用户进行身份验证和授权。

## 授权

授权是确定用户是否有权访问特定资源的过程。例如，您可能希望允许用户读取文件，但不允许写入文件。或者您可能希望允许用户删除记录，但不允许创建或更新它。

有两种常见的方式来实现授权：基于角色的访问控制和基于声明的访问控制。

通过基于角色的访问控制，用户被分配了一个角色。此角色定义允许用户执行的操作。例如，用户可能具有“管理员”角色，允许他们访问所有资源。或者用户可能具有“用户”角色，只允许他们访问某些资源。

使用基于声明的访问控制，一个用户被分配一个或多个声明。每个声明都定义了允许用户做什么。例如，用户可能拥有“can_read”的声明，允许他们阅读资源。或者用户可能拥有“can_write”的声明，允许他们写入资源。

要实施授权，您需要决定使用哪种方法。我们建议对大多数应用程序使用基于角色的访问控制。

一旦决定使用哪种方法，就需要实施它。

如果您使用基于角色的访问控制，则需要在数据库中创建角色表。该表将包含您的用户可以分配的角色。每个角色都有一个名称和描述。

您还需要创建一个用户表。该表将包含您系统中的用户。每个用户都有一个 role_id 对应于 roles 表中的一个角色。

要授权用户，您需要根据角色表检查他们的 role_id。例如，如果用户试图访问他们无权访问的资源，您可以返回错误：

```
if (user.role_id != 1) {
  return res.status(403).send('You do not have permission to access this resource');
}
```

如果您使用基于声明的访问控制，则需要在数据库中创建一个声明表。该表将包含可以分配给您的用户的声明。每个声明都会有一个名称和一个描述。

您还需要创建一个 user_claims 表。该表将包含每个用户的声明。每个声明都有一个 user_id 对应于 users 表中的用户。

要授权用户，您需要检查他们的 user_claims 表。例如，如果用户试图访问他们无权访问的资源，您可以返回错误：

```
if (!user_claims.includes('can_read')) {
  return res.status(403).send('You do not have permission to access this resource');
}
```

## 结论

后端应用程序的身份验证和授权有多种实现方式。在本文中，我们概述了最常用的方法，并为每种方法提供了一些实用技巧。

我们希望本文对您有所帮助，并且您现在对如何为后端应用程序实施身份验证和授权有了更好的了解。