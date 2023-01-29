---
title: Hello World in Spring Boot
description: 
published: true
date: 2023-01-29T14:55:20.203Z
tags: 
editor: markdown
dateCreated: 2023-01-29T14:55:20.203Z
---



# Introduction

Spring Boot is an open source Java-based framework used to create a micro-service. It is used to create stand-alone, production-grade applications that you can "just run". It simplifies the development of web applications and reduces the time and effort required to create a production-ready application.

# Hello World in Spring Boot

Creating a "Hello World" application in Spring Boot is a great way to get started with the framework. This tutorial will walk you through the steps of creating a simple "Hello World" application in Spring Boot.

## Prerequisites

Before you begin, you will need to have the following installed:

- Java 8 or higher
- Apache Maven 3.3 or higher
- Spring Boot 2.0 or higher

## Create a Maven Project

The first step is to create a Maven project. To do this, open a terminal window and run the following command:

```
mvn archetype:generate -DgroupId=com.example -DartifactId=hello-world -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This will create a new Maven project with the following structure:

```
hello-world
├── pom.xml
└── src
    ├── main
    │   └── java
    │       └── com
    │           └── example
    │               └── App.java
    └── test
        └── java
            └── com
                └── example
                    └── AppTest.java
```

## Add Dependencies

Next, you will need to add the Spring Boot dependencies to the `pom.xml` file. Open the `pom.xml` file and add the following dependencies:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

## Create the Main Class

Now, you will need to create the main class for the application. Create a new class called `HelloWorldApplication.java` in the `src/main/java/com/example` directory and add the following code:

```java
@SpringBootApplication
public class HelloWorldApplication {

    public static void main(String[] args) {
        SpringApplication.run(HelloWorldApplication.class, args);
    }

}
```

## Create the Controller

Next, you will need to create a controller to handle the incoming requests. Create a new class called `HelloWorldController.java` in the `src/main/java/com/example` directory and add the following code:

```java
@RestController
public class HelloWorldController {

    @RequestMapping("/")
    public String helloWorld() {
        return "Hello World!";
    }

}
```

## Run the Application

Finally, you can run the application by executing the following command in the terminal window:

```
mvn spring-boot:run
```

Once the application is running, you can access it at `http://localhost:8080`. You should see the message "Hello World!" displayed in the browser.

# Additional Informations

Spring Boot makes it easy to create stand-alone, production-grade applications that you can "just run". It simplifies the development of web applications and reduces the time and effort required to create a production-ready application.

# Warnings

Be sure to use the correct version of Java and Apache Maven when creating a Spring Boot application.
{.is-warning}

# Dangers

Do not forget to add the Spring Boot dependencies to the `pom.xml` file.
{.is-danger}

# Summary

This tutorial walks through the steps of creating a simple "Hello World" application in Spring Boot. !!!SUMMARY!!! Create a Maven project, add dependencies, create the main class, create the controller, and run the application. !!!TAGS!!! spring-boot, hello-world, tutorial.