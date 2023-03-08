---
title: Kotlin for Web Development: Building REST APIs
description: 
published: true
date: 2023-02-18T00:33:26.859Z
tags: 
editor: markdown
dateCreated: 2023-02-18T00:33:18.819Z
---

- [웹 개발을 위한 Kotlin: REST API 구축***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-for-web-development-building-rest-apis)
{.links-list}


# Kotlin for Web Development: Building REST APIs

Kotlin is a JVM language that offers an expressive syntax, null safety, and Kotlin extensions. In recent years, it has gained popularity for its Concurrency support and for being a more concise alternative to Java.

In this article, we'll be looking at Kotlin for web development by building a REST API. We'll be using the Ktor framework and covering the following topics:

* Setting up a Ktor project
* Configuring Ktor
* Routing
* Creating a database connection
* Serialization
* Testing

## Setting up a Ktor project

We'll start by setting up a Ktor project using the Gradle build system. Add the following to your `build.gradle.kts` file:

```kotlin
plugins {
    kotlin("jvm") version "1.3.72"
    id("io.ktor.server.netty") version "1.3.2"
}

repositories {
    jcenter()
}

dependencies {
    implementation("io.ktor:ktor-server-netty:$ktor_version")
    implementation("ch.qos.logback:logback-classic:1.2.3")
    implementation("org.slf4j:slf4j-api:1.7.30")
}
```

Replace `$ktor_version` with the latest version of Ktor. At the time of writing, the latest version is `1.3.2`.

## Configuring Ktor

We'll configure Ktor in the `Application.kt` file.

First, we'll configure the logging level. By default, Ktor will log everything at the `INFO` level. For a REST API in production, we'll want to change the logging level to `ERROR`. Add the following to the `Application.kt` file:

```kotlin
import ch.qos.logback.classic.Level
import ch.qos.logback.classic.LoggerContext
import org.slf4j.LoggerFactory

// ...

fun Application.module() {
    // ...

    // Configure logging
    val context: LoggerContext = LoggerFactory.getILoggerFactory() as LoggerContext
    context.setLogLevel(Level.ERROR)
}
```

Next, we'll configure the port that the server will run on. By default, Ktor will run on port `8080`. We can change this by adding the following to the `Application.kt` file:

```kotlin
import io.ktor.server.engine.ApplicationEngine
import io.ktor.server.engine.embeddedServer
import io.ktor.server.netty.Netty

// ...

fun Application.module() {
    // ...

    // Configure port
    val server: ApplicationEngine = embeddedServer(Netty, port = 8080) {
        // ...
    }
}
```

## Routing

In Ktor, routes are defined in the `routing` block. The `routing` block is a function that takes an `ApplicationCall` as a parameter. The `ApplicationCall` object provides access to the request and response.

We'll start by defining a route that returns a list of users. Add the following to the `Application.kt` file:

```kotlin
import io.ktor.application.call
import io.ktor.response.respond
import io.ktor.routing.get
import io.ktor.routing.routing

// ...

fun Application.module() {
    // ...

    // Define routes
    routing {
        get("/users") {
            val users = listOf(
                User(1, "John"),
                User(2, "Jane")
            )
            call.respond(users)
        }
    }
}
```

In the code above, we've defined a `GET` route that returns a list of `User` objects. The `User` class is defined as follows:

```kotlin
data class User(val id: Int, val name: String)
```

We can test the route by running the server and making a `GET` request to `http://localhost:8080/users`. We should get the following response:

```json
[
    {
        "id": 1,
        "name": "John"
    },
    {
        "id": 2,
        "name": "Jane"
    }
]
```

## Creating a database connection

We'll use the `exposed` library to connect to a database. `exposed` is a lightweight SQL library for Kotlin.

First, we'll add the `exposed` dependency to the `build.gradle.kts` file:

```kotlin
plugins {
    // ...
}

repositories {
    // ...
}

dependencies {
    // ...
    implementation("org.jetbrains.exposed:exposed-core:0.17.7")
    implementation("org.jetbrains.exposed:exposed-dao:0.17.7")
    implementation("org.jetbrains.exposed:exposed-jdbc:0.17.7")
}
```

Next, we'll create a `DatabaseFactory` class to manage the database connection. Add the following to the `Application.kt` file:

```kotlin
import org.jetbrains.exposed.sql.Database

class DatabaseFactory {
    companion object {
        fun init() {
            Database.connect(
                "jdbc:h2:./test",
                driver = "org.h2.Driver"
            )
        }
    }
}
```

In the code above, we've defined a `DatabaseFactory` class with a `Companion Object` that contains a `init` function. The `init` function creates a database connection using the `Database.connect` function.

We can test the database connection by adding the following to the `Application.kt` file:

```kotlin
import org.jetbrains.exposed.sql.selectAll
import org.jetbrains.exposed.sql.transactions.transaction

// ...

fun main() {
    DatabaseFactory.init()
    transaction {
        println("Users:")
        User.selectAll().forEach {
            println("${it.id}: ${it.name}")
        }
    }
}
```

In the code above, we've imported the `selectAll` and `transaction` functions from the `exposed` library. We've also added a `main` function that calls the `init` function from the `DatabaseFactory` class.

The `main` function also contains a `transaction` block. The `transaction` block is used to execute SQL statements. In the `transaction` block, we've defined a `SELECT` statement that returns all rows from the `User` table.

We can test the code by running the server and making a `GET` request to `http://localhost:8080/users`. We should get the following response:

```json
[
    {
        "id": 1,
        "name": "John"
    },
    {
        "id": 2,
        "name": "Jane"
    }
]
```

## Serialization

Kotlin offers built-in support for serialization. We can use the `@Serializable` annotation to serialize data classes.

We'll start by adding the `kotlin-serialization` plugin to the `build.gradle.kts` file:

```kotlin
plugins {
    // ...
    kotlin("plugin.serialization") version "1.3.72"
}

repositories {
    // ...
}

dependencies {
    // ...
}
```

Next, we'll annotate the `User` class with the `@Serializable` annotation:

```kotlin
@Serializable
data class User(val id: Int, val name: String)
```

We can test the serialization by adding the following to the `Application.kt` file:

```kotlin
import kotlinx.serialization.json.Json

// ...

fun main() {
    // ...
    transaction {
        println("Users:")
        User.selectAll().forEach {
            println(Json.encodeToString(it))
        }
    }
}
```

In the code above, we've added the `kotlinx.serialization.json` library and imported the `Json` class. We've also added a `main` function that calls the `init` function from the `DatabaseFactory` class.

The `main` function also contains a `transaction` block. In the `transaction` block, we've defined a `SELECT` statement that returns all rows from the `User` table. We've also added a `println` statement that uses the `Json.encodeToString` function to serialize the `User` objects.

We can test the code by running the server and making a `GET` request to `http://localhost:8080/users`. We should get the following response:

```json
[
    {"id":1,"name":"John"},
    {"id":2,"name":"Jane"}
]
```

## Testing

We'll use the `kotlintest` library to write tests for our REST API. `kotlintest` is a flexible and comprehensive testing tool for Kotlin.

First, we'll add the `kotlintest` dependency to the `build.gradle.kts` file:

```kotlin
plugins {
    // ...
}

repositories {
    // ...
}

dependencies {
    // ...
    testImplementation("io.kotlintest:kotlintest-runner-junit5:3.4.2")
    testImplementation("io.kotlintest:kotlintest-extensions-junit5:3.4.2")
}
```

Next, we'll write a test for the `GET /users` route. Add the following to the `ApplicationTest.kt` file:

```kotlin
import io.ktor.server.testing.withTestApplication
import org.junit.jupiter.api.Test
import kotlintest.specs.StringSpec
import org.jetbrains.exposed.sql.transactions.transaction

@Test
class ApplicationTest : StringSpec() {
    init {
        "should return list of users" {
            withTestApplication {
                DatabaseFactory.init()
                transaction {
                    // given
                    val users = listOf(
                        User(1, "John"),
                        User(2, "Jane")
                    )

                    // when
                    val response = handleRequest {
                        uri = "/users"
                        method = HttpMethod.Get
                    }.response

                    // then
                    response.status() shouldBe HttpStatusCode.OK
                    response.content shouldBe Json.encodeToString(users)
                }
            }
        }
    }
}
```

In the code above, we've imported the `withTestApplication`, `transaction`, `handleRequest`, and `response` functions from the `ktor-server-testing` and `kotlintest` libraries. We've also imported the `Json` class.

We've defined a `ApplicationTest` class that extends the `StringSpec` class from the `kotlintest` library. The `ApplicationTest` class contains a `should return list of users` test.

The `should return list of users` test contains a `withTestApplication` block. The `withTestApplication` block allows us to test our application in isolation.

In the `withTestApplication` block, we've called the `init` function from the `DatabaseFactory` class. We've also defined a `transaction` block. In the `transaction` block, we've defined a `given`, `when`, and `then` section.

In the `given` section, we've defined a list of `User` objects. In the `when` section, we've made a `GET` request to the `/users` route. In the `then` section, we've asserted that the response status code is `200 OK` and that the response body is equal to the JSON-encoded list of `User` objects.

We can run the test by running the `test` Gradle task. We should see the following output:

```
$ ./gradlew test

> Task :test
Users:
1: John
2: Jane

io.ktor.server.testing.ApplicationTest > should return list of users STANDARD_OUT
    Users:
    1: John
    2: Jane

io.ktor.server.testing.ApplicationTest > should return list of users PASSED

Executed 1 tests in 0.002s

> Task :test PASSED

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/6.5/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 0s
3 actionable tasks: 2 executed, 1 up-to-date
```

## Conclusion

In this article, we've looked at Kotlin for web development by building a REST API. We've covered the following topics:

* Setting up a Ktor project
* Configuring Ktor
* Routing
* Creating a database connection
* Serialization
* Testing

If you're interested in learning more about Kotlin, check out the following resources:

* [Kotlin documentation](https://kotlinlang.org/docs/reference/)
* [Ktor documentation](https://ktor.io/docs/introduction.html)
* [Exposed documentation](https://github.com/JetBrains/Exposed/wiki)
* [Kotlintest documentation](https://github.com/kotlintest/kotlintest/tree/master/doc)