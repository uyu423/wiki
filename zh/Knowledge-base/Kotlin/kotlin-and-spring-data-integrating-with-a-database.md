---
title: Kotlin 和 Spring Data：与数据库集成
description: 
published: true
date: 2023-02-07T00:55:23.444Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:55:17.809Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Spring Data: Integrating with a Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-integrating-with-a-database)
{.links-list}


# Kotlin 和 Spring Data：与数据库集成

Kotlin 是一种 JVM 语言，近年来因其简洁的语法和与 Java 的互操作性而受到欢迎。 Spring Data 是在 Spring 应用程序中处理数据的强大工具。在本文中，我们将了解如何使用 Kotlin 和 Spring Data 来处理数据库。

我们将首先创建一个 Kotlin 数据类来表示一个数据库实体。然后我们将创建一个 Spring Data Repository 接口来管理我们的数据。我们将使用 JpaRepository 实现此接口。最后，我们将使用我们的存储库来查询和更新我们的数据。

## 创建数据类

我们将首先创建一个 Kotlin 数据类来表示一个数据库实体。我们称我们的类为“User”。我们的“User”类将具有三个属性：“id”、“name”和“email”。


```kotlin
data class User(
        val id: Long,
        val name: String,
        val email: String
)
```

## 创建存储库

接下来，我们将创建一个 Spring Data Repository 接口来管理我们的数据。我们将我们的接口称为“UserRepository”。我们的 UserRepository 将扩展 JpaRepository 并使用我们的 User 数据类进行参数化。

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

## 实现存储库

我们将使用 `JpaRepository` 实现我们的 `UserRepository` 接口。我们将把我们的 `JpaRepository` 注入到我们的 Kotlin `Application` 类中。

```kotlin
@SpringBootApplication
class Application {

    @Autowired
    lateinit var userRepository: UserRepository

    fun main(args: Array<String>) {
        SpringApplication.run(Application::class.java, *args)
    }
}
```

## 查询存储库

现在我们有了我们的 UserRepository，我们可以用它来查询我们的数据库。我们将从查找数据库中的所有用户开始。

```kotlin
val users = userRepository.findAll()
```

我们还可以通过他们的“id”找到用户。

```kotlin
val user = userRepository.findById(1L)
```

## 更新用户

我们可以使用我们的 UserRepository 来更新数据库中的 User。我们将从找到要更新的用户开始。然后我们将更新他们的 `name` 和 `email` 属性。最后，我们将保存我们的更改。

```kotlin
val user = userRepository.findById(1L)

user.name = "John Doe"
user.email = "john.doe@example.com"

userRepository.save(user)
```

## 删除用户

我们可以使用我们的 UserRepository 从我们的数据库中删除一个 User。我们将从找到要删除的用户开始。然后我们将从我们的数据库中删除它们。

```kotlin
val user = userRepository.findById(1L)

userRepository.delete(user)
```

## 结论

在本文中，我们了解了如何使用 Kotlin 和 Spring Data 来处理数据库。我们创建了一个 Kotlin 数据类来表示一个数据库实体。我们还创建了一个 Spring Data Repository 接口来管理我们的数据。我们已经使用 JpaRepository 实现了这个接口。最后，我们使用我们的存储库来查询和更新我们的数据。