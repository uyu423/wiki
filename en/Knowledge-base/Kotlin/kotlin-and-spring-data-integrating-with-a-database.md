---
title: Kotlin and Spring Data: Integrating with a Database
description: 
published: true
date: 2023-02-07T00:55:19.416Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:55:17.813Z
---

- [Kotlin y Spring Data: integración con una base de datos***Spanish** document is available*](/es/Knowledge-base/Kotlin/kotlin-and-spring-data-integrating-with-a-database)
{.links-list}
- [Kotlin 和 Spring Data：与数据库集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-spring-data-integrating-with-a-database)
{.links-list}
- [Kotlin 및 Spring 데이터: 데이터베이스와 통합***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-spring-data-integrating-with-a-database)
{.links-list}


# Kotlin and Spring Data: Integrating with a Database

Kotlin is a JVM language that has gained popularity in recent years for its concise syntax and interoperability with Java. Spring Data is a powerful tool for working with data in Spring applications. In this article, we'll see how to use Kotlin and Spring Data to work with a database.

We'll start by creating a Kotlin data class to represent a database entity. Then we'll create a Spring Data Repository interface to manage our data. We'll implement this interface with a JpaRepository. Finally, we'll use our Repository to query and update our data.

## Creating a Data Class

We'll start by creating a Kotlin data class to represent a database entity. We'll call our class `User`. Our `User` class will have three properties: `id`, `name`, and `email`.


```kotlin
data class User(
        val id: Long,
        val name: String,
        val email: String
)
```

## Creating a Repository

Next, we'll create a Spring Data Repository interface to manage our data. We'll call our interface `UserRepository`. Our `UserRepository` will extend `JpaRepository` and be parameterized with our `User` data class.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

## Implementing the Repository

We'll implement our `UserRepository` interface with a `JpaRepository`. We'll inject our `JpaRepository` into our Kotlin `Application` class.

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

## Querying the Repository

Now that we have our `UserRepository`, we can use it to query our database. We'll start by finding all users in our database.

```kotlin
val users = userRepository.findAll()
```

We can also find a user by their `id`.

```kotlin
val user = userRepository.findById(1L)
```

## Updating a User

We can use our `UserRepository` to update a `User` in our database. We'll start by finding the user we want to update. Then we'll update their `name` and `email` properties. Finally, we'll save our changes.

```kotlin
val user = userRepository.findById(1L)

user.name = "John Doe"
user.email = "john.doe@example.com"

userRepository.save(user)
```

## Deleting a User

We can use our `UserRepository` to delete a `User` from our database. We'll start by finding the user we want to delete. Then we'll delete them from our database.

```kotlin
val user = userRepository.findById(1L)

userRepository.delete(user)
```

## Conclusion

In this article, we've seen how to use Kotlin and Spring Data to work with a database. We've created a Kotlin data class to represent a database entity. We've also created a Spring Data Repository interface to manage our data. We've implemented this interface with a JpaRepository. Finally, we've used our Repository to query and update our data.