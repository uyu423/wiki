---
title: 030: Developing and deploying a Spring Boot application with Gradle
description: 
published: true
date: 2023-02-03T22:32:32.053Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:32:27.165Z
---

- [030: Desarrollo e implementación de una aplicación Spring Boot con Gradle***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/030-developing-and-deploying-a-spring-boot-application-with-gradle)
{.links-list}
- [030：使用 Gradle 开发和部署 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/030-developing-and-deploying-a-spring-boot-application-with-gradle)
{.links-list}
- [030: Gradle로 Spring Boot 애플리케이션 개발 및 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/030-developing-and-deploying-a-spring-boot-application-with-gradle)
{.links-list}


# 030: Developing and deploying a Spring Boot application with Gradle

Spring Boot is a popular Java framework for developing web applications. It makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run."

In this post, we'll go over how to develop and deploy a Spring Boot application using Gradle. We'll start by setting up our project, then we'll write our code and package it into a jar file. Finally, we'll deploy our application to a server.

## Setting up our project

The first thing we need to do is set up our project. We'll create a new directory for our project and initialize a Gradle build script.

```
$ mkdir my-spring-boot-app
$ cd my-spring-boot-app
$ gradle init
```

Next, we need to add the Spring Boot dependency to our build script. We'll do this by adding the following line to our `build.gradle` file:

```
dependencies {
    compile 'org.springframework.boot:spring-boot-starter-web'
}
```

## Writing our code

Now that our project is set up, we can start writing our code. We'll create a simple Spring Boot application that prints "Hello, world!"

First, we'll create a file called `HelloWorldController.java` in our `src/main/java` directory. This file will contain our controller:

```java
package com.example.myapp;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }

}
```

Next, we'll create a file called `Application.java` in our `src/main/java` directory. This file will contain our main application class:

```java
package com.example.myapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Packaging our application

Now that our code is written, we need to package it into a jar file. We can do this by running the `gradle build` command. This will create a jar file in our `build/libs` directory.

## Deploying our application

Now that our application is packaged, we can deploy it to a server. We'll use the `java -jar` command to run our jar file:

```
$ java -jar build/libs/my-spring-boot-app.jar
```

Our application will start up on port 8080. We can access it by going to http://localhost:8080 in our browser.

## Conclusion

In this post, we've gone over how to develop and deploy a Spring Boot application using Gradle. We've set up our project, written our code, packaged it into a jar file, and deployed it to a server.