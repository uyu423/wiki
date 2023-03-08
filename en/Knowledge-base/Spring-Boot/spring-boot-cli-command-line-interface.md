---
title: Spring Boot CLI Command Line Interface
description: 
published: true
date: 2023-02-17T18:15:00.175Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:23:38.605Z
---

- [Spring Boot CLI 명령줄 인터페이스***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-cli-command-line-interface)
{.links-list}
- [Spring Boot CLI コマンドライン インターフェイス***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-boot-cli-command-line-interface)
{.links-list}
- [Spring Boot CLI 命令行界面***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-cli-command-line-interface)
{.links-list}



# Spring Boot CLI Command Line Interface

The Spring Boot CLI is a command line interface used to quickly build Spring-based applications. It provides a fast way to generate a Spring project, complete with all the necessary dependencies. 

The Spring Boot CLI is an important tool for developers who want to get up and running with Spring quickly. In this article, we'll take a look at how to use the Spring Boot CLI to quickly create a Spring project. We'll also discuss some of the features that the Spring Boot CLI provides.

## Getting Started

In order to use the Spring Boot CLI, you will need to have the following installed:

* Java 8 or higher
* Apache Maven 3.3.9 or higher

You can check if you have these installed by running the following commands:

```
java -version
mvn -version
```

If you don't have these installed, you can follow the instructions [here](https://spring.io/guides/gs/getting-started-maven/).

Once you have these installed, you can download the Spring Boot CLI by visiting [this link](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.3.1.RELEASE/spring-boot-cli-2.3.1.RELEASE-bin.zip).

Once you have downloaded the Spring Boot CLI, you will need to unzip it and add the `bin` directory to your `PATH`. This will allow you to run the `spring` command from any directory.

## Creating a Spring Project

Now that you have the Spring Boot CLI installed, let's use it to create a Spring project. We'll create a project that uses the [Web](https://start.spring.io/#dependencies=web) and [JPA](https://start.spring.io/#dependencies=data-jpa) dependencies.

To do this, we'll use the `spring init` command. This command will create a Spring project with the specified dependencies. The `-d` flag is used to specify the dependencies that we want to include in our project. In our case, we want to include the Web and JPA dependencies. We'll also specify the `-b` flag to indicate that we want to use the [bootstrap](https://getbootstrap.com/) dependency.

```
spring init -d=web,data-jpa -b
```

This will create a directory called `my-project` with the following structure:

```
my-project
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           └── myproject
    │   │               └── MyprojectApplication.java
    │   └── resources
    │       └── application.properties
    └── test
        └── java
            └── com
                └── example
                    └── myproject
                        └── MyprojectApplicationTests.java
```

The `pom.xml` file contains the project's dependencies. The `src/main/java` directory contains the project's Java source code. The `src/test/java` directory contains the project's tests. The `src/main/resources` directory contains project resources such as property files.

## Running the Application

Now that we have a Spring project, let's run it to see what it does. To do this, we'll use the `spring run` command. This command will compile and run the application.

```
spring run src/main/java/com/example/myproject/MyprojectApplication.java
```

This will start the application on port 8080. You can view the application by visiting [http://localhost:8080](http://localhost:8080).

## SpringBoot CLI Commands

While the `spring run` command is useful for quickly running an application, the Spring Boot CLI provides many other commands that can be used for different tasks. We'll briefly discuss some of the most useful commands below.

### `spring boot`

The `spring boot` command can be used to create a new Spring Boot application. This command will generate a new project with the specified dependencies. This is the same command that we used to create our project in the previous section.

### `spring clean`

The `spring clean` command can be used to clean the project's build directory. This is useful if you want to remove any compiled files or other artifacts that are not needed.

### `spring run`

The `spring run` command can be used to compile and run the application. This is the same command that we used to run our application in the previous section.

### `spring test`

The `spring test` command can be used to run the project's tests. This is useful for verifying that the application is functioning correctly.

### `spring jar`

The `spring jar` command can be used to package the application into a JAR file. This is useful for deploying the application to a server.

### `spring war`

The `spring war` command can be used to package the application into a WAR file. This is useful for deploying the application to a server.

### `spring help`

The `spring help` command can be used to display a list of all of the available commands. This is useful for getting a quick overview of all of the commands that are available.

## Conclusion

In this article, we've discussed how to use the Spring Boot CLI to quickly create Spring-based applications. We've also covered some of the most useful commands that the Spring Boot CLI provides.