---
title: 062: Building a REST API with Spring Boot
description: 
published: true
date: 2023-02-03T02:57:33.237Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:57:28.433Z
---

- [062: Creación de una API REST con Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/062-building-a-rest-api-with-spring-boot)
{.links-list}
- [062：使用 Spring Boot 构建 REST API***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/062-building-a-rest-api-with-spring-boot)
{.links-list}
- [062: Spring Boot로 REST API 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/062-building-a-rest-api-with-spring-boot)
{.links-list}


# 062: Building a REST API with Spring Boot 

In this post, we'll learn how to build a REST API with Spring Boot.

We'll start by creating a new Spring Boot project. Then, we'll add a dependency to our project that will allow us to create a REST API.

Next, we'll create a controller that will handle HTTP requests to our API. Finally, we'll test our API using Postman.

## Creating a Spring Boot Project 

First, we'll need to create a new Spring Boot project. We can do this using the Spring Initializr.

We'll need to specify the following information:

- Group: com.example
- Artifact: demo
- Name: DemoApplication
- Description: Demo project for 062
- Package Name: com.example.demo
- Packaging: Jar
- Java Version: 8
- Language: Kotlin
- Boot Version: 2.1.5

![spring-initializr](https://i.imgur.com/eU0mhVv.png)

Once we've filled out the form, we can click "Generate Project." This will download a ZIP file containing our project.

## Adding a Dependency 

Next, we'll need to add a dependency to our project. This dependency will allow us to create a REST API.

We can do this by adding the following to our build.gradle file:

```groovy
dependencies {
    ...
    compile("org.springframework.boot:spring-boot-starter-web")
}
```

## Creating a Controller 

Now that we have our project set up, we can start creating our API.

We'll start by creating a controller. This controller will handle HTTP requests to our API.

We can do this by creating a new Kotlin file called DemoController.kt in the com.example.demo package.

```kotlin
package com.example.demo

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class DemoController {

    @GetMapping("/")
    fun index(): String {
        return "Hello, world!"
    }
}
```

In this file, we've created a controller with a single endpoint. This endpoint will return the string "Hello, world!" when accessed.

## Testing Our API 

Now that we've created our API, we can test it to make sure it works as expected.

We can do this using Postman. Postman is a tool that allows us to send HTTP requests to our API.

First, we'll need to start our application. We can do this by running the following command:

```
./gradlew bootRun
```

Once our application has started, we can send an HTTP GET request to the "/" endpoint. We should see the string "Hello, world!" in the response body.

![postman](https://i.imgur.com/zgWVLCg.png)

## Conclusion 

In this post, we've learned how to build a REST API with Spring Boot. We've created a new project, added a dependency, created a controller, and tested our API.