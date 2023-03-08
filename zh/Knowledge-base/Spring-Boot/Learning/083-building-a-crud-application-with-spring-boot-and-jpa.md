---
title: 083：使用 Spring Boot 和 JPA 构建 CRUD 应用程序
description: 
published: true
date: 2023-02-05T13:32:25.336Z
tags: 
editor: markdown
dateCreated: 2023-02-05T13:32:22.879Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [083: Building a CRUD Application with Spring Boot and JPA***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/083-building-a-crud-application-with-spring-boot-and-jpa)
{.links-list}


083：使用 Spring Boot 和 JPA 构建 CRUD 应用程序
================================================ ======

在本文中，我们将学习如何使用 Spring Boot 和 JPA 构建 CRUD 应用程序。

我们将首先创建一个资源表示类。此类将用于表示我们在应用程序中的数据。

接下来，我们将创建一个存储库接口。该接口将用于访问我们的数据。

最后，我们将创建一个控制器。该控制器将用于处理 HTTP 请求和响应。

创建资源表示类
------------------------------------------

第一步是创建资源表示类。此类将用于表示我们在应用程序中的数据。

我们将从创建一个名为“User”的类开始。此类将具有三个字段：`id`、`name` 和 `email`。


    公共课用户{
    
        私人长号；
        私有字符串名称；
        私人字符串电子邮件；
    
        // 获取器和设置器
    
    }


创建存储库接口
----------------------------------

接下来，我们将创建一个存储库接口。该接口将用于访问我们的数据。

我们将从创建一个名为 UserRepository 的接口开始。该接口将扩展“JpaRepository”。 `JpaRepository` 是一个 Spring Data JPA 接口，为我们提供 CRUD 操作。


    public interface UserRepository extends JpaRepository<User, Long> {
    
    }


创建控制器
----------------------

最后，我们将创建一个控制器。该控制器将用于处理 HTTP 请求和响应。

我们将从创建一个名为“UserController”的类开始。这个类将有两个方法：`getAllUsers` 和 `createUser`。

`getAllUsers` 方法将用于处理对 `/users` 的 GET 请求。此方法将返回数据库中所有用户的列表。

`createUser` 方法将用于处理对 `/users` 的 POST 请求。此方法将在数据库中创建一个新用户。


    @RestController
    公共类用户控制器 {
    
        @Autowired
        私有用户存储库用户存储库；
    
        @GetMapping("/用户")
        公共列表<用户> getAllUsers() {
            返回 userRepository.findAll();
        }
    
        @PostMapping("/用户")
        public User createUser(@RequestBody User user) {
            返回 userRepository.save(user);
        }
    
    }


测试应用程序
----------------------

现在我们已经创建了资源表示类、存储库接口和控制器，可以开始测试我们的应用程序了。

我们将从创建一个“User”对象开始。


    用户 user = new User();
    user.setName("李四");
    user.setEmail("john.doe@example.com");


接下来，我们将调用 `createUser` 方法。


    user = userController.createUser(用户);


最后，我们将调用“getAllUsers”方法。


    List<User> users = userController.getAllUsers();
    assertThat（用户）.contains（用户）；


如果一切顺利，您应该会看到以下输出：


    [
        {
            “编号”：1，
            "name": "约翰·杜伊",
            “电子邮件”：“john.doe@example.com”
        }
    ]


您可以在 GitHub 上找到此示例的完整源代码。