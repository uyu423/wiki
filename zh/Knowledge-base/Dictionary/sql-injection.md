---
title: SQL Injection
description: 
published: true
date: 2023-02-07T07:17:43.820Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:17:42.074Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [SQL Injection***English** document is available*](/en/Knowledge-base/Dictionary/sql-injection)
{.links-list}


# 概述
SQL 注入是一种网络攻击，涉及将恶意代码插入到数据库查询中。它用于访问或修改存储在数据库中的敏感数据。

# 描述
SQL 注入是一种利用数据库查询漏洞的攻击形式。这是一种注入攻击，其中将恶意 SQL 代码插入到查询中以获取对敏感数据的访问或修改。攻击者可以使用此访问权限窃取数据、修改数据，甚至从数据库中删除数据。

SQL 注入攻击可用于绕过身份验证机制、执行任意代码，甚至获得对底层操作系统的访问权限。攻击者还可以使用 SQL Injection 修改数据库记录，例如更改用户密码或删除记录。

SQL 注入攻击通常通过向 Web 应用程序发送恶意输入来执行。该输入随后由应用程序处理并传递给数据库。如果应用程序没有正确验证输入，恶意代码可能会被数据库执行。

# 历史
SQL 注入攻击自互联网早期就已存在。 1998 年，第一次公开报道的 SQL 注入攻击发生在一家名为 Security Dynamics 的公司开发的 Web 应用程序上。从那时起，SQL 注入攻击变得越来越普遍和复杂。

# 特征
SQL 注入攻击通常通过向 Web 应用程序发送恶意输入来执行。恶意输入然后由应用程序处理并传递到数据库。如果应用程序没有正确验证输入，恶意代码可能会被数据库执行。

SQL 注入攻击可用于绕过身份验证机制、执行任意代码，甚至获得对底层操作系统的访问权限。攻击者还可以使用 SQL Injection 修改数据库记录，例如更改用户密码或删除记录。

# 例子
SQL 注入攻击的一个示例是攻击者向 Web 应用程序发送恶意输入。恶意输入然后由应用程序处理并传递到数据库。如果应用程序没有正确验证输入，恶意代码可能会被数据库执行。

例如，攻击者可以将以下输入发送到 Web 应用程序：

```
SELECT * FROM users WHERE username='admin' OR '1'='1'
```

此输入将导致应用程序执行以下查询：

```
SELECT * FROM users WHERE username='admin' OR '1'='1'
```

此查询将返回数据库中的所有用户，无论他们的用户名如何。

# 优点和缺点
SQL 注入攻击有利也有弊。一方面，它们可用于访问敏感数据或修改数据库中的记录。另一方面，它们也可用于对系统造成重大损害，例如删除数据或执行任意代码。

# 争议
SQL 注入攻击是安全社区中一个有争议的话题。一些人认为它们是必要的邪恶，因为它们可用于访问敏感数据并修改数据库中的记录。其他人则认为应该不惜一切代价避免使用它们，因为它们可以用来对系统造成重大损害。

# 相关技术
SQL 注入攻击与其他类型的网络攻击有关，例如跨站点脚本 (XSS) 和跨站点请求伪造 (CSRF)。这些攻击还可用于获取敏感数据的访问权限或修改数据库中的记录。

# 题外话
SQL 注入攻击是一种可用于访问或修改存储在数据库中的敏感数据的攻击类型。它们从互联网早期就已经存在，并且变得越来越普遍和复杂。虽然它们可用于访问敏感数据或修改数据库中的记录，但它们也可用于对系统造成重大损害。

# 其他的
可以通过正确验证用户输入来防止 SQL 注入攻击。这可以通过使用准备好的语句和参数化查询来完成，这确保用户提供的输入被视为数据而不是可执行代码。此外，应对 Web 应用程序进行漏洞测试并定期修补以防止 SQL 注入攻击。