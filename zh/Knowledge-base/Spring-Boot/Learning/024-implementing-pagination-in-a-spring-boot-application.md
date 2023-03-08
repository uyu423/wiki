---
title: 024: 在 Spring Boot 应用程序中实现分页
description: 
published: true
date: 2023-02-03T16:32:20.214Z
tags: 
editor: markdown
dateCreated: 2023-02-03T16:32:18.617Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [024: Implementing pagination in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/024-implementing-pagination-in-a-spring-boot-application)
{.links-list}


分页是 Web 应用程序中的常见功能。它用于将大型数据集分解为更小、更易于管理的块。 Spring Boot 使得在 Web 应用程序中实现分页变得容易。

在本文中，我们将学习如何在 Spring Boot 应用程序中实现分页。我们将从创建一个简单的 Spring Boot 应用程序开始。然后，我们将向应用程序添加分页功能。

创建 Spring Boot 应用程序

我们将使用 Spring Initializr 来创建我们的 Spring Boot 应用程序。转到 Spring Initializr 网站并选择以下选项：

* 项目：Maven项目
* 语言：Java
* 春季启动版本：2.1.3

单击“生成”按钮生成项目。

生成项目后，将其导入您喜欢的 IDE。我正在使用 Eclipse。

添加分页功能

我们将使用 org.springframework.data.domain 包中的 Pageable 接口在我们的应用程序中实现分页。

首先，我们需要将 spring-data-commons 依赖项添加到我们的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-commons</artifactId>
    <version>2.1.3.RELEASE</version>
</dependency>
```

接下来，我们将创建一个简单的 RestController，它带有一个返回用户列表的方法：

```java
@RestController
public class UserController {

    @GetMapping("/users")
    public List<User> getUsers() {
        // Return a list of users
    }
}
```

现在，我们将分页功能添加到 getUsers() 方法。我们将使用 Pageable 接口来指定页面大小和页码。 Pageable 接口有两个实现：PageRequest 和 Slice。我们将在示例中使用 PageRequest 实现。

```java
@GetMapping("/users")
public List<User> getUsers(Pageable pageable) {
    // Return a list of users
}
```

我们还可以指定页面大小和页码作为查询参数：

```java
@GetMapping("/users")
public List<User> getUsers(
        @RequestParam(name = "page", defaultValue = "0") int page,
        @RequestParam(name = "size", defaultValue = "10") int size) {
    // Return a list of users
}
```

在上面的示例中，我们指定了默认页面大小为 10，默认页码为 0。

测试分页功能

我们可以通过使用页面和大小查询参数向 /users 端点发送 GET 请求来测试分页功能。

例如，以下请求将返回页面大小为 10 的用户的第一页：

```
GET /users?page=0&size=10
```

以下请求将返回页面大小为 10 的用户的第二页：

```
GET /users?page=1&size=10
```

等等。

附加信息

Pageable 接口还有其他几种方法可用于自定义分页行为。有关详细信息，请参阅 Pageable 接口的 JavaDocs。

警告

实现分页时，重要的是要确保页面大小不会太大。如果页面大小太大，可能会导致 OutOfMemoryErrors。

危险

实现分页时，重要的是要确保页面大小不要太小。如果页面太小，可能会导致太多的数据库查询。