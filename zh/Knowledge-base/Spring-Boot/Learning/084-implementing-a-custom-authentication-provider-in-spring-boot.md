---
title: 084：在 Spring Boot 中实现自定义身份验证提供程序
description: 
published: true
date: 2023-02-05T14:32:26.057Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:32:24.485Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [084: Implementing a Custom Authentication Provider in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/084-implementing-a-custom-authentication-provider-in-spring-boot)
{.links-list}


# 在 Spring Boot 中实现自定义身份验证提供程序

当涉及到 Spring Boot 中的身份验证时，有几种不同的方法可以解决。在本文中，我们将了解如何实现自定义身份验证提供程序。

## 什么是身份验证提供程序？

身份验证提供程序是一种处理用户身份验证过程的软件。在 Web 应用程序的上下文中，这通常意味着验证用户是否提供了正确的凭据（用户名和密码），如果是，则允许他们访问应用程序。

## 为什么使用自定义身份验证提供程序？

您可能希望使用自定义身份验证提供程序的原因有以下几个：

* 您想使用不同于 Spring Boot 开箱即用的身份验证方法（例如，您想使用 LDAP 而不是数据库）。
* 您想要向身份验证过程添加额外的功能（例如，您想要记录所有失败的登录尝试）。
* 您希望更好地控制身份验证过程的工作方式（例如，您希望能够自定义显示给用户的错误消息）。

## 如何实现自定义身份验证提供程序

实现自定义身份验证提供程序实际上非常简单。您需要做的就是创建一个实现 org.springframework.security.authentication.AuthenticationProvider 接口的类。

这是一个简单的例子：

```java
public class MyAuthenticationProvider implements AuthenticationProvider {

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        // TODO: Implement authentication logic here
        return null;
    }

    @Override
    public boolean supports(Class<?> authentication) {
        // TODO: Implement authentication support logic here
        return false;
    }
}
```

有两个方法需要实现：

* `authenticate()`：这是实际的身份验证逻辑所在的位置。该方法将“Authentication”对象作为参数并返回一个“Authentication”对象。
* `supports()`：此方法用于确定 `AuthenticationProvider` 是否支持给定的 `Authentication` 对象。

## 配置身份验证提供程序

一旦实现了“AuthenticationProvider”，下一步就是在 Spring Boot 中配置它。这可以通过将以下内容添加到“application.properties”文件来完成：

```properties
spring.security.authentication-provider.class=com.example.MyAuthenticationProvider
```

## 测试身份验证提供程序

要测试身份验证提供程序，您可以在测试方法上使用“@WithMockUser”注释。这将创建一个具有给定用户名和密码的模拟用户，可用于对身份验证提供程序进行身份验证。

这是一个简单的例子：

```java
@Test
@WithMockUser(username="test", password="test")
public void testAuthentication() {
    // TODO: Implement authentication test here
}
```

## 结论

在这篇文章中，我们研究了如何在 Spring Boot 中实现自定义身份验证提供程序。我们还了解了如何配置它以及如何测试它。