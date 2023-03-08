---
title: 058：在 Spring Boot 应用程序中实现安全性
description: 
published: true
date: 2023-02-04T21:32:30.237Z
tags: 
editor: markdown
dateCreated: 2023-02-04T21:32:24.982Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [058: Implementing Security in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/058-implementing-security-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用程序中实现安全性

作为 Java 开发人员，您可能熟悉 Spring 框架。 Spring Boot 是 Spring 框架的扩展，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

在本文中，我们将了解如何在 Spring Boot 应用程序中实现安全性。我们将从查看可以在 Spring Boot 应用程序中实现的不同类型的安全性开始。然后，我们将了解如何配置和使用 Spring Security 框架来保护我们的应用程序。

## 安全类型

在 Spring Boot 应用程序中可以实现两种主要的安全类型：身份验证和授权。

身份验证是验证用户是否与他们声称的身份相符的过程。授权是确定用户是否有权访问特定资源的过程。

在 Spring Boot 应用程序中，身份验证通常由登录表单处理。用户输入他们的用户名和密码，Spring Security 验证凭据是否有效。

授权通常通过为用户分配角色来处理。例如，您可能有一个管理员角色和一个普通用户角色。管理员可能比普通用户有权访问更多资源。

## 配置 Spring 安全

Spring Security 是一个提供身份验证和授权服务的框架。在 Spring Boot 应用程序中配置和使用它很容易。

要将 Spring Security 添加到您的应用程序，请将以下依赖项添加到您的构建文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

添加依赖项后，默认情况下将启用 Spring Security。默认情况下，Spring Security 将使用内存中的身份验证。这意味着无需配置数据库或任何其他外部服务。

要配置 Spring Security，您可以将 @Configuration 类添加到您的应用程序。此类可用于配置 Spring Security 的各个方面，例如允许访问应用程序的用户以及他们拥有的角色。

## 验证用户

当用户尝试访问受保护的资源时，他们将被重定向到登录页面。在此页面上，他们将输入他们的用户名和密码。

然后 Spring Security 将对用户进行身份验证。如果凭据有效，用户将被重定向到他们试图访问的资源。如果凭据无效，用户将被重定向到错误页面。

## 授权用户

一旦用户通过身份验证，Spring Security 将需要授权用户才能访问受保护的资源。

授权通常通过为用户分配角色来完成。例如，您可能有一个管理员角色和一个普通用户角色。管理员可能比普通用户有权访问更多资源。

您可以通过将 @RolesAllowed 注释添加到控制器或服务方法来配置用户具有的角色。例如：

```java
@Service
public class MyService {

    @RolesAllowed("ADMIN")
    public void doSomething() {
        // ...
    }
}
```

在此示例中，doSomething() 方法只能由具有 ADMIN 角色的用户访问。

## 结论

在本文中，我们了解了如何在 Spring Boot 应用程序中实现安全性。我们已经研究了可以实现的不同类型的安全性，并了解了如何配置和使用 Spring Security 框架。