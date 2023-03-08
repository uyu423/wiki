---
title: 052：使用 Spring Boot 和 Spring MVC 构建搜索引擎优化 (SEO) 友好的网站
description: 
published: true
date: 2023-02-02T18:57:28.135Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:57:26.476Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [052: Building a search engine optimization (SEO) friendly website using Spring Boot and Spring MVC***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/052-building-a-search-engine-optimization-seo-friendly-website-using-spring-boot-and-spring-mvc)
{.links-list}


## 介绍

搜索引擎优化 (SEO) 是提高网站在搜索引擎上的排名的做法。排名越高，人们就越有可能找到该网站。

影响网站排名的因素有很多，包括内容的质量、网站的结构以及网站的编码方式。

在这篇文章中，我们将重点介绍如何使用对搜索引擎友好的 Spring Boot 和 Spring MVC 编写网站代码。

## 什么是 Spring Boot？

Spring Boot 是一个框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

Spring Boot 包含许多使创建和运行 Web 应用程序变得容易的功能，包括：

- 嵌入式 Tomcat 或 Jetty 服务器
- 支持 Thymeleaf、FreeMarker 和其他模板引擎
- 自动配置
- 自动生成项目文档

## 什么是Spring MVC？

Spring MVC 是一个用于构建 Web 应用程序的框架。它建立在 Spring 框架之上，为 Web 应用程序开发提供统一的方法。

Spring MVC 包含许多使开发 Web 应用程序变得容易的功能，包括：

- 用于处理请求和响应的简单、一致的模型
- 灵活的视图解析机制
- 支持多视图技术
- 可插入的本地化机制

## 创建一个 Spring Boot Web 应用程序

我们将使用 Spring Initializr 创建一个 Spring Boot Web 应用程序。

转到 Spring Initializr 网站 (https://start.spring.io/) 并填写表单以创建一个新项目。

![Spring Initializr](https://i.imgur.com/hm3Y6uq.png)

选择以下选项：

- 项目：摇篮项目
- 语言：Java
- 春季启动版本：2.1.4

单击“生成项目”以下载项目。

## 将项目导入 Eclipse

将项目作为 Gradle 项目导入到 Eclipse 中。

## 创建控制器

控制器是 Spring MVC 应用程序的核心。他们负责处理请求和响应。

在我们的示例中，我们将创建一个控制器来处理对“/”URL 的请求。

在 com.example.demo 包中创建一个新类并将其命名为“HelloController.java”。

将以下代码添加到类中：

```java
package com.example.demo;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @RequestMapping("/")
    @ResponseBody
    public String index() {
        return "Hello, world!";
    }

}
```

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello, world!</title>
    </head>
    <body>
        <p>Hello, world!</p>
    </body>
</html>
```@RequestMapping``` 注释将对“/”URL 的请求映射到 index() 方法。

```properties
spring.thymeleaf.prefix=classpath:/templates/
spring.thymeleaf.suffix=.html
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
spring.thymeleaf.cache=false
```html
<!DOCTYPE html>
<html>
    <头>
        <title>你好，世界！</title>
    </头>
    <正文>
        <p>你好，世界！</p>
    </body>
</html>
```
./gradlew bootRun
```属性
spring.thymeleaf.prefix=类路径：/模板/
spring.thymeleaf.suffix=.html
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8 编码
spring.thymeleaf.content-type=文本/html
spring.thymeleaf.cache=false
```
curl http://localhost:8080/
```
./gradlew bootRun
```

要从 Eclipse 运行应用程序，请右键单击项目并选择“Run As -> Spring Boot App”。

## 测试应用程序

我们可以通过向“/”URL 发送请求来测试应用程序。

要从命令行测试应用程序，我们可以使用 curl 命令。

```
卷曲 http://localhost:8080/
```

要从 Eclipse 测试应用程序，我们可以使用内置浏览器。

右键单击 HelloController.java 文件并选择“Run As -> Spring Boot App”。

应用程序将启动，“/”URL 将在浏览器中打开。

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 Spring MVC 创建一个搜索引擎优化 (SEO) 友好的网站。

我们已经了解了如何创建处理请求和响应的控制器，以及如何创建由模板引擎处理的视图。

我们还了解了如何使用属性文件配置应用程序。