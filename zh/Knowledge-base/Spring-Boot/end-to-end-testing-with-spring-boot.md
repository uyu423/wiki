---
title: 使用 Spring Boot 进行端到端测试
description: 
published: true
date: 2023-02-01T17:40:25.579Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:40:23.618Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [End-to-end Testing with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}


# 使用 Spring Boot 进行端到端测试

在构建 Web 应用程序时，端到端 (E2E) 测试是开发过程的关键部分。根据定义，E2E 测试是一种从头到尾涵盖整个应用程序的测试。

在传统的 Web 应用程序中，前端代码会向后端服务器发出请求，然后后端服务器会处理请求并返回响应。对于 Spring Boot 应用程序，前端代码仍然发出请求，但后端服务器现在是 Spring Boot 应用程序。

E2E 测试很重要，因为它允许开发人员测试整个应用程序，从用户界面 (UI) 到后端服务器。它还允许开发人员测试应用程序在部署到生产环境时的工作方式。

有许多不同的 E2E 测试框架可用，但在本文中，我们将重点介绍 Spring Boot 及其提供的 E2E 测试框架。

## 什么是 Spring Boot？

Spring Boot 是一个允许开发人员快速创建和部署基于 Spring 的应用程序的框架。它提供了许多使开发和部署更容易的功能，例如：

- 嵌入式 Tomcat 服务器
- 自动配置
- 入门模板

Spring Boot 是开发 E2E 测试的绝佳选择，因为它可以轻松创建和部署基于 Spring 的应用程序。

## 端到端测试框架是什么？

E2E 测试框架是一组允许开发人员快速创建和运行 E2E 测试的工具。它基于 JUnit 测试框架，并提供了许多使 E2E 测试更容易的功能，例如：

- @SpringBootTest 注释，可用于配置 Spring Boot 应用程序以进行测试
- @WebIntegrationTest 注释，可用于配置 Web 服务器以进行测试
- 可用于在 Spring 应用程序上下文中模拟 beans 的 @MockBean 注释

E2E 测试框架是开发 E2E 测试的绝佳选择，因为它可以轻松创建和运行 E2E 测试。

## 创建端到端测试

现在让我们看看如何使用端到端测试框架创建端到端测试。我们将测试一个简单的 Spring Boot 应用程序，该应用程序具有一个返回用户列表的端点。

我们需要做的第一件事是创建一个新的 JUnit 测试类并用@SpringBootTest 注释它：

```java
@SpringBootTest
public class UserControllerTest {

}
```

@SpringBootTest 注释用于配置 Spring Boot 应用程序以进行测试。

接下来，我们需要创建一个测试方法，并用@Test注解它：

```java
@Test
public void testGetUsers() {

}
```

@Test 注解用于将方法标记为测试方法。

在测试方法中，我们需要创建一个 UserController 实例并调用 getUsers() 方法：

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
}
```

getUsers() 方法返回用户列表，因此我们可以断言该列表不为空：

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).isNotEmpty();
}
```

我们还可以断言该列表包含预期数量的用户：

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).hasSize(2);
}
```

最后，我们可以断言该列表包含预期用户：

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users)
        .contains(new User("user1@example.com", "User 1"),
                  new User("user2@example.com", "User 2"));
}
```

完整的端到端测试如下图：

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## 运行 E2E 测试

要运行 E2E 测试，我们只需将测试类作为 JUnit 测试运行：

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## 结论

在本文中，我们了解了如何使用 E2E 测试框架创建和运行 E2E 测试。我们还看到了如何使用 @SpringBootTest 和 @Test 注释来配置 Spring Boot 应用程序并将方法标记为测试方法。