---
title: 使用 Spring Boot 构建 RESTful 服务
description: 
published: true
date: 2023-01-31T16:38:08.920Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:38:07.198Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Building RESTful Services with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/building-restful-services-with-spring-boot)
{.links-list}


# 使用 Spring Boot 构建 RESTful 服务

在本文中，我们将了解使用 Spring Boot 构建 RESTful Web 服务的一些最佳实践。

我们将涵盖以下主题：

* 设计一个 REST API
* 设计 RESTful 端点的最佳实践
* 使用 Spring Boot 实现 REST API
* 测试 REST API
* 保护 REST API

## 设计 REST API

在设计 REST API 时，重要的是要考虑以下因素：

* 您的 API 将公开的资源
* 可以对这些资源执行的操作
* 资源之间的关系

您的 API 的设计方式应使开发人员易于使用。它应该易于理解和使用，并且应该保持一致。

在为您的 API 设计端点时，您应该使用一致的命名约定。例如，您可以使用以下约定：

```
/{resource}/{id}
```

其中 {resource} 是资源的名称，{id} 是资源的标识符。

以一致的方式使用 HTTP 方法也是一个好主意。例如，您可以使用以下约定：

```
GET /{resource}/{id}
POST /{resource}
PUT /{resource}/{id}
DELETE /{resource}/{id}
```

其中 GET 用于检索资源，POST 用于创建资源，PUT 用于更新资源，DELETE 用于删除资源。

## 设计 RESTful 端点的最佳实践

在为您的 API 设计端点时，请牢记一些最佳实践：

* 对资源使用复数名称
* 使用连字符分隔单词
* 使用小写字母
* 以一致的方式使用 HTTP 方法
* 以一致的方式使用 HTTP 状态代码

## 使用 Spring Boot 实现 REST API

现在我们已经介绍了设计 REST API 的一些最佳实践，让我们来看看如何使用 Spring Boot 实现 REST API。

Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。我们将使用 Spring Boot 创建一个公开单一资源的简单 API。

### 依赖项

首先，我们需要将以下依赖项添加到我们的项目中：

* spring-boot-starter-data-rest
* spring-boot-starter-data-jpa
* spring-boot-starter-web

### 实体

让我们从创建一个实体开始。我们将为我们的实体名称使用以下约定：

```
{resource}_{operation}
```

其中 {resource} 是资源的名称，{operation} 是对资源执行的操作。

对于我们的示例，我们将创建一个名为“user_create”的实体。

```java
@Entity
@Table(name = "user_create")
public class UserCreate {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @Column(name = "email")
    private String email;

    // getters and setters
}
```

### 仓库

接下来，我们将为我们的实体创建一个存储库。我们将为我们的存储库名称使用以下约定：

```
{resource}Repository
```

其中 {resource} 是资源的名称。

对于我们的示例，我们将创建一个名为 UserCreateRepository 的存储库。

```java
public interface UserCreateRepository extends JpaRepository<UserCreate, Long> {

}
```

### 服务

现在，我们将为我们的实体创建一个服务。我们将为我们的服务名称使用以下约定：

```
{resource}Service
```

其中 {resource} 是资源的名称。

对于我们的示例，我们将创建一个名为“UserCreateService”的服务。

```java
@Service
public class UserCreateService {

    @Autowired
    private UserCreateRepository userCreateRepository;

    public UserCreate create(UserCreate userCreate) {
        return userCreateRepository.save(userCreate);
    }
}
```

### 控制器

最后，我们将为我们的实体创建一个控制器。我们将为我们的控制器名称使用以下约定：

```
{resource}Controller
```

其中 {resource} 是资源的名称。

对于我们的示例，我们将创建一个名为 UserCreateController 的控制器。

```java
@RestController
@RequestMapping("/user-creates")
public class UserCreateController {

    @Autowired
    private UserCreateService userCreateService;

    @PostMapping
    public UserCreate create(@RequestBody UserCreate userCreate) {
        return userCreateService.create(userCreate);
    }
}
```

这就是我们使用 Spring Boot 创建一个简单的 REST API 所需要做的全部工作。

## 测试 REST API

测试 REST API 时，需要注意以下几点：

* 端点应该是可访问的
* 端点应该返回预期的数据
* 端点应返回预期的 HTTP 状态代码

要测试我们的示例 API，我们可以使用以下 curl 命令：

```
# create a user
curl -X POST -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john.doe@example.com"}' http://localhost:8080/user-creates

# get a user
curl -X GET http://localhost:8080/user-creates/1

# update a user
curl -X PUT -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john.doe@example.com"}' http://localhost:8080/user-creates/1

# delete a user
curl -X DELETE http://localhost:8080/user-creates/1
```

## 保护 REST API

在保护 REST API 时，需要牢记以下几点：

* 验证
* 授权
* 速率限制

身份验证是验证用户身份的过程。授权是确定允许用户做什么的过程。速率限制是限制用户可以发出的请求数量的过程。

保护 REST API 的方法有很多，但最流行的方法之一是使用 JSON Web 令牌 (JWT)。

为了使用 JWT 保护我们的示例 API，我们可以使用以下 curl 命令：

```
# login
curl -X POST -H "Content-Type: application/json" -d '{"username":"john.doe","password":"password"}' http://localhost:8080/auth/login

# get a user
curl -X GET -H "Authorization: Bearer <token>" http://localhost:8080/user-creates/1

# logout
curl -X POST -H "Authorization: Bearer <token>" http://localhost:8080/auth/logout
```

## 结论

在本文中，我们介绍了使用 Spring Boot 构建 RESTful Web 服务的一些最佳实践。我们了解了如何设计 REST API、如何使用 Spring Boot 实现 REST API、如何测试 REST API 以及如何保护 REST API。