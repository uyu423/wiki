---
title: 004：使用 Spring Boot 和 Spring MVC 构建 REST API
description: 
published: true
date: 2023-02-03T07:36:48.417Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:36:46.721Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [004: Building REST APIs with Spring Boot and Spring MVC***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/004-building-rest-apis-with-spring-boot-and-spring-mvc)
{.links-list}


# 004：使用 Spring Boot 和 Spring MVC 构建 REST API

在本文中，我们将学习如何使用 Spring Boot 和 Spring MVC 构建 REST API。

我们将从创建一个简单的 Spring Boot 应用程序开始。然后，我们将添加一个控制器来公开一些 REST 端点。最后，我们将使用 Postman 测试我们的 API。

## 创建 Spring Boot 应用程序

首先，我们需要创建一个 Spring Boot 应用程序。我们可以使用 Spring Initializr 来做到这一点。

转到 http://start.spring.io/ 并选择以下选项：

- 使用 Java 和 Spring Boot 2.0 生成 Maven 项目
- 包装：罐
- Java 版本：8
- 组：com.example
- 神器：演示
- 名称：DemoApplication
- 描述：Spring Boot REST API 演示
- 包名：com.example.demo

单击“生成项目”以下载项目。

解压缩 zip 文件并在您喜欢的 IDE 中打开项目。

## 添加控制器

接下来，我们将添加一个控制器来公开一些 REST 端点。

首先，我们将创建一个名为 com.example.demo.controller 的新包。然后，我们将在该包中创建一个名为“DemoController”的新类。

我们的控制器将具有以下端点：

- `GET /`: 欢迎信息
- `GET /hello`: 一句问候
- `POST /greeting`：带有自定义消息的问候语

这是我们控制器的代码：

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoController {

    @GetMapping("/")
    public String index() {
        return "Welcome to the Spring Boot REST API!";
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }

    @PostMapping("/greeting")
    public String greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return "Hello, " + name + "!";
    }

}
```

让我们分解一下上面代码中发生的事情。

首先，我们使用“@RestController”注释将此类指定为控制器。

然后，我们使用“@GetMapping”和“@PostMapping”注释将 HTTP GET 和 POST 请求映射到控制器中的特定方法。

最后，我们使用 @RequestParam 注释从请求中提取查询参数。在这种情况下，我们正在提取“名称”参数。如果未指定 `name` 参数，我们将使用默认值 `World`。

## 测试API

现在我们已经设置了控制器，让我们使用 Postman 测试我们的 API。

首先，我们需要启动我们的应用程序。我们可以通过将“DemoApplication”类作为 Java 应用程序运行来实现。

应用程序启动后，我们可以使用 Postman 向我们的 API 发送请求。

让我们向 `/` 端点发送一个 GET 请求：

![获取请求](https://i.imgur.com/LNcuFtD.png)

如您所见，我们收到了一条欢迎消息作为回应。

让我们向 /hello 端点发送 GET 请求：

![你好请求](https://i.imgur.com/VywYbnK.png)

如您所见，我们收到了问候语作为回应。

最后，让我们向“/greeting”端点发送一个 POST 请求：

![后请求](https://i.imgur.com/EC4nUg4.png)

如您所见，我们收到了带有自定义消息的问候语作为响应。

## 结论

在本文中，我们学习了如何使用 Spring Boot 和 Spring MVC 构建 REST API。

我们首先创建一个简单的 Spring Boot 应用程序。然后，我们添加了一个控制器来公开一些 REST 端点。最后，我们使用 Postman 测试了我们的 API。