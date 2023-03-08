---
title: 深入探讨 Java 的安全管理器
description: 
published: true
date: 2023-01-31T19:17:35.773Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:17:34.235Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [A Deep Dive into Java's Security Manager***English** version of this document is available*](/en/Knowledge-base/Java/a-deep-dive-into-java-s-security-manager)
{.links-list}




Java 的安全管理器是 Java 平台安全架构的重要组成部分。它负责执行 Java 应用程序或小程序的安全策略。

Security Manager 是一个 Java 类，它定义了一组方法，允许应用程序查询和请求访问系统资源的权限。它由 SecurityManager 类实现。

当不受信任的小程序或应用程序运行时，将调用安全管理器来检查小程序或应用程序是否具有访问其请求的系统资源的必要权限。如果小程序或应用程序没有必要的权限，安全管理器将抛出一个 SecurityException。

安全管理器还负责防止可能试图利用 Java 平台漏洞的恶意代码。例如，安全管理器可用于防止小程序读取或写入本地文件系统，或者防止与下载小程序的主机以外的主机建立网络连接。

为了使用安全管理器，应用程序或小程序必须首先调用 SecurityManager.getSecurityManager() 方法来获取对安全管理器的引用。然后可以使用安全管理器使用 checkPermission() 方法检查权限。

以下代码示例显示如何使用安全管理器检查是否允许小程序从本地文件系统读取文件：

```java
SecurityManager sm = System.getSecurityManager();
if (sm != null) {
  try {
    sm.checkPermission(new FilePermission("/tmp/foo.txt", "read"));
  } catch (SecurityException se) {
    // handle exception
  }
}
```

如果小程序或应用程序没有必要的权限，checkPermission() 方法将抛出一个 SecurityException。

需要注意的是，安全管理器并不是解决所有安全问题的灵丹妙药。请务必记住，安全管理器只能执行 Java 应用程序或小程序的安全策略。它无法抵御所有安全威胁。

例如，安全管理器无法防止缓冲区溢出攻击。缓冲区溢出攻击是一种将恶意代码注入程序以利用程序中的漏洞的攻击类型。

缓冲区溢出攻击通常用于控制程序或使程序崩溃。它们还可以用于将恶意代码注入到将在程序运行时执行的程序中。

为了防止缓冲区溢出攻击，重要的是使用一种不允许缓冲区溢出发生的语言。例如，Java 不允许发生缓冲区溢出，因为它使用一种称为边界检查的内存安全。

在开发 Java 应用程序时使用安全编码实践也很重要。安全 Java 开发的一些最佳实践包括：

- 使用安全框架，例如 Java 安全框架 (JSF)
- 使用安全策略文件来配置应用程序的安全设置
- 使用安全管理器来执行安全策略
- 使用密码学来保护数据
- 使用代码签名来确保代码的完整性

Java 安全管理器是 Java 平台安全架构的重要组成部分。它负责执行 Java 应用程序或小程序的安全策略。通过使用安全管理器，开发人员可以帮助保护他们的应用程序免受恶意代码和可能被攻击者利用的漏洞的侵害。