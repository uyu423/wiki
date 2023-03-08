---
title: 008: Creating and using templates with Thymeleaf
description: 
published: true
date: 2023-02-03T08:17:38.000Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:17:33.083Z
---

- [008: Creación y uso de plantillas con Thymeleaf***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/008-creating-and-using-templates-with-thymeleaf)
{.links-list}
- [008：使用 Thymeleaf 创建和使用模板***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/008-creating-and-using-templates-with-thymeleaf)
{.links-list}
- [008: Thymeleaf로 템플릿 생성 및 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/008-creating-and-using-templates-with-thymeleaf)
{.links-list}


# Introduction 

In this post, we will be discussing how to create and use templates with Thymeleaf.

Thymeleaf is a modern server-side Java template engine that enables us to create HTML, XML, and other markup languages in a well-formed and structured way.

It is an open-source project that is licensed under the Apache License 2.0.

# What is a Template? 

A template is a file that contains the static parts of your website or application, as well as placeholder variables for dynamic content.

A template engine is a tool that takes your static template files and replaces the placeholder variables with actual values, resulting in a file that can be served to a user.

# Why Use Templates? 

Templates are a great way to separate the static parts of your website or application from the dynamic parts.

This separation makes it easier to manage your code, as well as make changes to the static parts of your site without affecting the dynamic content.

It also makes it easier to cache the static parts of your site, which can improve performance.

# What is Thymeleaf? 

Thymeleaf is a template engine for Java.

It is an open-source project that is licensed under the Apache License 2.0.

Thymeleaf enables us to create HTML, XML, and other markup languages in a well-formed and structured way.

It also has excellent support for internationalization (i18n) and localization (l10n).

Thymeleaf is used in many popular Java web frameworks, such as Spring MVC, Spring Boot, and Vaadin.

# Thymeleaf Syntax 

Thymeleaf has two types of syntax: Standard and OGNL.

Standard syntax is the default syntax mode and is used to create well-formed and structured HTML, XML, and other markup languages.

OGNL syntax is an extension of the standard syntax and is used to access objects in the Thymeleaf context.

# Creating a Template 

We can create a Thymeleaf template in any text editor.

For this example, we will create a template called "hello.html" in the src/main/resources/templates directory.

hello.html

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

In the template above, we have a variable called "message" that will be replaced with a value when the template is processed.

# Rendering a Template 

We can render a Thymeleaf template in a Java application using the ThymeleafTemplateEngine class.

First, we need to create a ThymeleafTemplateEngine instance:

```java
ThymeleafTemplateEngine templateEngine = new ThymeleafTemplateEngine();
```

Then, we can render the template by passing the template name and a map of variables to the renderTemplate() method:

```java
String result = templateEngine.renderTemplate("hello.html", ImmutableMap.of("message", "Hello, World!"));
```

# Conclusion 

In this post, we have learned how to create and use templates with Thymeleaf.

We have also learned about the different types of syntax that Thymeleaf supports.

If you want to learn more about Thymeleaf, please check out the following resources:

- The Thymeleaf website: https://www.thymeleaf.org/
- The Thymeleaf GitHub repository: https://github.com/thymeleaf/thymeleaf
- The Thymeleaf user guide: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html