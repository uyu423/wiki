---
title: Getting started with Spring Boot
description: 
published: true
date: 2023-01-29T17:28:00.631Z
tags: 
editor: markdown
dateCreated: 2023-01-29T17:28:00.631Z
---


# What is Spring Boot?

Spring Boot is a Java-based framework used for creating microservices. It is developed by Pivotal Team and is used to build stand-alone and production-ready spring applications.

# Why use Spring Boot?

There are many reasons to use Spring Boot:

- It makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
- It provides opinionated 'starter' dependencies to simplify your build configuration.
- It avoids XML configuration and uses annotations to configure the application.
- It provides a CLI tool that can be used to quickly create and run Spring applications.

# How to get started with Spring Boot?

In this section, we will see how to get started with Spring Boot. We will create a simple Spring Boot application and run it on our local machine.

## Prerequisites

Before we get started, we need to have the following installed on our machine:

- Java 8 or above
- Maven 3.3.9 or above

## Create a Spring Boot project

We can create a Spring Boot project in many ways. In this section, we will use the Spring Initializr to create our project.

Go to the Spring Initializr website and enter the following details:

- Group: com.example
- Artifact: myproject
- Name: My Project
- Description: My Spring Boot project
- Package Name: com.example.myproject
- Packaging: Jar
- Java Version: 8
- Select the dependencies: Web, Lombok

Click on Generate Project to download the project.

## Import the project into your IDE

Import the project into your favorite IDE. I am using IntelliJ IDEA.

## Run the application

We can run the application using the following command:

```
./mvnw spring-boot:run
```

The application will start on port 8080. We can access it at http://localhost:8080.

## Conclusion

In this article, we saw how to get started with Spring Boot. We created a simple Spring Boot application and ran it on our local machine.