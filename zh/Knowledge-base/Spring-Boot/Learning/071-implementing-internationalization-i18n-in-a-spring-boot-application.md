---
title: 071：在 Spring Boot 应用程序中实现国际化 (i18n)
description: 
published: true
date: 2023-02-01T22:36:37.376Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:36:35.789Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [071: Implementing Internationalization (i18n) in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/071-implementing-internationalization-i18n-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用程序中实现国际化 (i18n)

国际化 (i18n) 是使您的应用程序支持多种语言的过程。这可能是一项复杂的任务，但 Spring Boot 使它变得容易得多。在本文中，我们将了解如何在 Spring Boot 应用程序中实现国际化。

## 什么是国际化？

国际化 (i18n) 是使您的应用程序支持多种语言的过程。这可能是一项复杂的任务，但 Spring Boot 使它变得容易得多。

## 为什么要使用 i18n？

您可能希望为您的应用程序添加 i18n 支持的原因有很多。也许您的用户遍布世界各地，并希望为他们提供本地化体验。或者您可能只是在构建个人项目并想了解如何添加 i18n 支持。不管是什么原因，i18n 都是一项值得拥有的宝贵技能。

## 如何在 Spring Boot 中实现国际化

Spring Boot 可以轻松地向您的应用程序添加 i18n 支持。在本节中，我们将看看如何做到这一点。

### 1. 添加国际化依赖

首先，您需要将 i18n 依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2.配置国际化属性

接下来，您需要在 application.properties 文件中配置 i18n 属性：

```properties
spring.mvc.locale=en
spring.messages.basename=i18n/messages
```

### 3. 创建国际化文件

现在您需要创建 i18n 文件。这些文件将包含为您的应用程序翻译的消息。您可以在 `src/main/resources/i18n` 中创建这些文件。

例如，假设您要支持英语和法语。您将创建以下文件：

- `messages_en.properties`
- `messages_fr.properties`

在这些文件中，您将为您的应用程序定义翻译后的消息。例如：

```properties
# messages_en.properties

greeting=Hello
```

```properties
# messages_fr.properties

greeting=Bonjour
```

### 4. 在代码中使用 i18n 消息

现在您已经配置了 i18n 文件，您可以在代码中使用翻译后的消息。例如，假设您有一个具有以下方法的控制器：

```java
@RequestMapping("/greeting")
public String greeting(Model model) {
    model.addAttribute("message", "greeting");
    return "greeting";
}
```

此方法将渲染 greeting.ftl 模板，并将 `message` 属性设置为 i18n 文件中的 `greeting` 键。因此，如果 `spring.mvc.locale` 属性设置为 `en`，则 `message` 属性将设置为 `Hello`。如果 `spring.mvc.locale` 属性设置为 `fr`，则 `message` 属性将设置为 `Bonjour`。

## 结论

在这篇文章中，我们研究了如何向 Spring Boot 应用程序添加 i18n 支持。 i18n 可能是一项复杂的任务，但 Spring Boot 使它变得容易得多。按照本文中的步骤，您可以轻松地为您的应用程序添加 i18n 支持。