---
title: 008：使用 Thymeleaf 创建和使用模板
description: 
published: true
date: 2023-02-03T08:17:34.700Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:17:33.076Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [008: Creating and using templates with Thymeleaf***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/008-creating-and-using-templates-with-thymeleaf)
{.links-list}


# 介绍

在这篇文章中，我们将讨论如何使用 Thymeleaf 创建和使用模板。

Thymeleaf 是一个现代服务器端 Java 模板引擎，它使我们能够以格式良好和结构化的方式创建 HTML、XML 和其他标记语言。

它是一个开源项目，根据 Apache License 2.0 获得许可。

# 什么是模板？

模板是一个文件，其中包含网站或应用程序的静态部分，以及动态内容的占位符变量。

模板引擎是一种工具，它获取静态模板文件并将占位符变量替换为实际值，从而生成可以提供给用户的文件。

# 为什么要使用模板？

模板是将网站或应用程序的静态部分与动态部分分开的好方法。

这种分离使您更容易管理您的代码，以及在不影响动态内容的情况下更改站点的静态部分。

它还可以更轻松地缓存站点的静态部分，从而提高性能。

# 什么是 Thymeleaf？

Thymeleaf 是 Java 的模板引擎。

它是一个开源项目，根据 Apache License 2.0 获得许可。

Thymeleaf 使我们能够以格式良好和结构化的方式创建 HTML、XML 和其他标记语言。

它还对国际化 (i18n) 和本地化 (l10n) 提供出色的支持。

Thymeleaf 用于许多流行的 Java Web 框架，例如 Spring MVC、Spring Boot 和 Vaadin。

# Thymeleaf 语法

Thymeleaf 有两种类型的语法：标准和 OGNL。

标准语法是默认的语法模式，用于创建结构良好的 HTML、XML 和其他标记语言。

OGNL 语法是标准语法的扩展，用于访问 Thymeleaf 上下文中的对象。

# 创建模板

我们可以在任何文本编辑器中创建 Thymeleaf 模板。

对于这个例子，我们将在 src/main/resources/templates 目录中创建一个名为“hello.html”的模板。

你好.html

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello, World!</title>
</head>
<body>
    <p th:text="${message}">Hello, World!</p>
</body>
</html>
```

在上面的模板中，我们有一个名为“message”的变量，当模板被处理时，它会被替换为一个值。

# 渲染模板

我们可以使用 ThymeleafTemplateEngine 类在 Java 应用程序中呈现 Thymeleaf 模板。

首先，我们需要创建一个 ThymeleafTemplateEngine 实例：

```java
ThymeleafTemplateEngine templateEngine = new ThymeleafTemplateEngine();
```

然后，我们可以通过将模板名称和变量映射传递给 renderTemplate() 方法来渲染模板：

```java
String result = templateEngine.renderTemplate("hello.html", ImmutableMap.of("message", "Hello, World!"));
```

# 结论

在本文中，我们学习了如何使用 Thymeleaf 创建和使用模板。

我们还了解了 Thymeleaf 支持的不同类型的语法。

如果您想了解有关 Thymeleaf 的更多信息，请查看以下资源：

- Thymeleaf 网站：https://www.thymeleaf.org/
- Thymeleaf GitHub 存储库：https://github.com/thymeleaf/thymeleaf
- Thymeleaf 用户指南：https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html