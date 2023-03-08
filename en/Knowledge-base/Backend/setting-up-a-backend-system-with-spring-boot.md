---
title: Setting up a Backend System with Spring Boot
description: 
published: true
date: 2023-02-17T18:01:02.232Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:31:47.650Z
---

- [Spring Boot로 백엔드 시스템 설정***Korean** version of this document is available*](/ko/Knowledge-base/Backend/setting-up-a-backend-system-with-spring-boot)
{.links-list}


# Setting up a Backend System with Spring Boot

Spring Boot is a popular Java-based framework used for developing web applications and microservices. It is developed by Pivotal and is available under the Apache License 2.0.

Spring Boot makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run." It takes an opinionated view of the Spring platform and third-party libraries so that you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

## Why Use Spring Boot?

There are many reasons to use Spring Boot when developing your next project, Here are some of the most important ones:

* It makes it easy to create stand-alone, production-grade Spring-based applications that can just be run.
* It takes an opinionated view of the Spring platform and third-party libraries, so you can get started with minimum fuss.
* It makes it easy to create production-ready applications.
* It provides a wide range of features that can be used in any project.
* It eliminates the need for XML configuration.

## Getting Started

In this section, we'll show you how to get started with Spring Boot. We'll begin by creating a new Spring Boot project using the [Spring Initializr](https://start.spring.io/). The Spring Initializr is a web-based tool that makes it easy to create a new Spring Boot project.

### Creating a New Project

To create a new Spring Boot project, you can use the Spring Initializr web tool. Go to the [Spring Initializr](https://start.spring.io/) website and select the following options:

* Project: `Gradle Project`
* Language: `Java`
* Spring Boot Version: `2.1.3`
* Project Metadata:
  * Group: `com.example`
  * Artifact: `myproject`
  * Name: `My Project`
  * Description: `A simple Spring Boot project`
  * Package Name: `com.example.myproject`
* Packaging: `Jar`
* Java Version: `8`
* Dependencies: `Web`

![Creating a new Spring Boot project](https://i.imgur.com/EuFcU3v.png)

Click the "Generate Project" button to download a zip file containing your new Spring Boot project.

### Importing the Project into your IDE

Spring Tool Suite (STS) is a popular IDE for developing Spring-based applications. In this section, we'll show you how to import the project into STS.

Start STS and go to `File` -> `Import...`. Select `Gradle Project` from the list of options and click `Next`.

![Importing a Gradle Project into STS](https://i.imgur.com/vYIT6TK.png)

Browse to the location of the project you downloaded from the Spring Initializr and click `Finish`.

![Selecting the project to import](https://i.imgur.com/WY6lNcu.png)

 STS will import the project and create a project structure similar to the following:

```
myproject
├── src
│   └── main
│       ├── java
│       │   └── com
│       │       └── example
│       │           └── myproject
│       │               └── Application.java
│       └── resources
│           ├── application.properties
│           └── static
│               └── index.html
├── build.gradle
└── settings.gradle
```

### Running the Application

You can run the application from the command line using the `gradlew` command:

```
$ ./gradlew bootRun
```

You can also run the application from your IDE. In STS, you can right-click on the `Application.java` file and select `Run As` -> `Spring Boot App`.

![Running the application in STS](https://i.imgur.com/DY0SVqf.png)

When the application is running, you can access the front page at [http://localhost:8080/](http://localhost:8080/).

![The front page of the application](https://i.imgur.com/i1aBG3g.png)

## Conclusion

In this article, we've shown you how to get started with Spring Boot. We've created a new project using the Spring Initializr and imported it into our IDE. We've also shown you how to run the application.