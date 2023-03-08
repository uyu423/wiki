---
title: 040：在 Spring Boot 应用程序中实现多语言支持
description: 
published: true
date: 2023-02-02T04:04:27.149Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:04:25.499Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [040: Implementing multi-language support in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/040-implementing-multi-language-support-in-a-spring-boot-application)
{.links-list}



# 在 Spring Boot 应用程序中实现多语言支持

国际化 (i18n) 是开发可适应特定当地语言和文化的产品或服务的过程，这一过程称为本地化 (l10n)。

借助 `spring-boot-starter-data-jpa` 和 `spring-boot-starter-thymeleaf` 启动器，Spring Boot 可以轻松地向您的应用程序添加 i18n 支持。

在这篇文章中，我们将介绍如何向 Spring Boot 应用程序添加 i18n 支持。我们将涵盖以下主题：

* 为 i18n 配置 Spring Boot
* 创建特定语言的消息文件
* 在您的视图中显示本地化消息
* 在您的应用程序中切换语言

## 为 i18n 配置 Spring Boot

首先，我们需要将 spring-boot-starter-data-jpa 和 spring-boot-starter-thymeleaf 启动器添加到我们的 pom.xml 中：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
</dependencies>
```

接下来，我们需要在我们的 application.properties 文件中配置 MessageSource bean：

```properties
spring.messages.basename=messages
```

`MessageSource` bean 负责解析消息文件中的消息。默认情况下，Spring Boot 将在 `src/main/resources` 目录中查找消息文件。

## 创建特定语言的消息文件

接下来，我们需要为我们想要支持的每种语言创建消息文件。消息文件必须命名为“messages_[lang].properties”，其中“[lang]”是语言的 [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 代码.

例如，如果我们想要支持英语和法语，我们将创建以下消息文件：

*`messages_en.properties`
* `messages_fr.properties`

每个消息文件都将包含可由“MessageSource”bean 解析的每条消息的键值对。例如，我们的“messages_en.properties”文件可能如下所示：

```properties
greeting=Hello, world!
```

我们的“messages_fr.properties”文件可能如下所示：

```properties
greeting=Bonjour, monde!
```

## 在您的视图中显示本地化消息

现在我们已经设置了我们的消息文件，我们可以开始在我们的视图中显示本地化的消息。

在 Thymeleaf 中，我们可以使用 `# {.links-list}` 语法从我们的消息文件中解析消息。例如，如果我们想显示来自 `messages_en.properties` 文件的 `greeting` 消息，我们可以执行以下操作：

```html
<p th:text="#{greeting}">Hello, world!</p>
```

如果我们想显示来自 `messages_fr.properties` 文件的 `greeting` 消息，我们可以执行以下操作：

```html
<p th:text="#{greeting}">Bonjour, monde!</p>
```

## 在你的应用程序中切换语言

现在我们可以在我们的视图中显示本地化消息，我们需要一种在语言之间切换的方法。

有很多方法可以做到这一点，但一种简单的方法是向我们应用程序的 queryString 添加一个 lang 参数。例如，如果我们想切换到法语，我们可以执行以下操作：

```
http://localhost:8080/?lang=fr
```

然后我们可以使用 lang 参数在我们的 LocaleResolver bean 中设置 Locale。例如，我们可以将以下内容添加到我们的 application.properties 文件中：

```properties
spring.mvc.locale-resolver=org.springframework.web.servlet.i18n.SessionLocaleResolver
```

然后将以下内容添加到我们的“LocaleResolver”bean：

```java
@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver localeResolver = new SessionLocaleResolver();
    localeResolver.setDefaultLocale(Locale.ENGLISH);
    return localeResolver;
}
```

现在，当我们访问 `http://localhost:8080/?lang=fr` 时，我们的应用程序将切换到法语并显示来自 `messages_fr.properties` 文件的 `greeting` 消息。

## 结论

在本文中，我们介绍了如何向 Spring Boot 应用程序添加 i18n 支持。我们已经了解了如何为 i18n 配置 Spring Boot，如何创建特定于语言的消息文件，如何在我们的视图中显示本地化消息，以及如何在我们的应用程序中切换语言。