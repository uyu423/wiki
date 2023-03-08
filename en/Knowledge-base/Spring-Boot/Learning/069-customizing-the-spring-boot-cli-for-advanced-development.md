---
title: 069: Customizing the Spring Boot CLI for Advanced Development
description: 
published: true
date: 2023-02-05T03:32:23.186Z
tags: 
editor: markdown
dateCreated: 2023-02-05T03:32:21.538Z
---

- [069: Personalización de Spring Boot CLI para desarrollo avanzado***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/069-customizing-the-spring-boot-cli-for-advanced-development)
{.links-list}
- [069：为高级开发定制 Spring Boot CLI***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/069-customizing-the-spring-boot-cli-for-advanced-development)
{.links-list}
- [069: 고급 개발을 위한 Spring Boot CLI 사용자 정의***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/069-customizing-the-spring-boot-cli-for-advanced-development)
{.links-list}


# Customizing the Spring Boot CLI for Advanced Development

The Spring Boot CLI is a great tool for quickly bootstrapping Spring applications. It allows you to create stand-alone Spring-based applications that can be run from the command line without the need for a web server.

In this post, we'll take a look at how to customize the Spring Boot CLI for advanced development. We'll cover how to install the CLI, how to create and run Spring Boot applications, and how to customize the CLI for your own development needs.

## Installing the Spring Boot CLI

The Spring Boot CLI is a command-line tool that can be used to quickly create and run Spring Boot applications. It is available as a standalone executable JAR file or as a Homebrew package.

To install the Spring Boot CLI, first download the latest version of the CLI from the Spring Boot website. Then, unzip the downloaded file and add the `spring-boot-cli/bin` directory to your `PATH`.

Alternatively, if you are using Homebrew, you can install the Spring Boot CLI by running the following command:

```
$ brew tap pivotal/tap
$ brew install springboot
```

## Creating a Spring Boot Application

Now that we have the Spring Boot CLI installed, let's create a simple Spring Boot application. We'll start by creating a new directory for our project:

```
$ mkdir my-app
$ cd my-app
```

Next, we'll create a new file called `application.properties` in our project directory. This file will contain our Spring Boot application's configuration. We'll set the `spring.main.banner-mode` property to `off` so that the Spring Boot banner is not displayed when our application is run:

```
spring.main.banner-mode=off
```

Now, we can create our Spring Boot application. We'll use the `spring` command to create a new `@SpringBootApplication` class:

```
$ spring init -n com.example.myapp -d web my-app.jar
```

This will create a new `my-app.jar` file in our project directory. We can run our application by executing the following command:

```
$ java -jar my-app.jar
```

Our application will start up and be accessible at `http://localhost:8080`.

## Customizing the Spring Boot CLI

The Spring Boot CLI provides a number of options for customizing its behavior. These options can be specified either on the command line or in the `spring` configuration file.

The `spring` configuration file is a YAML file that is read by the Spring Boot CLI when it starts up. This file can be used to specify options for the `spring` command, such as the default project directory and the default package name.

To create a `spring` configuration file, create a new file called `.spring-configuration.yaml` in your home directory. The contents of this file will be read by the Spring Boot CLI when it starts up.

Here is an example `spring` configuration file:

```yaml
spring:
  project:
    default-project-dir: ~/projects
  package:
    default-package-name: com.example
```

This file sets the default project directory to `~/projects` and the default package name to `com.example`.

Now, when we create a new Spring Boot application, the `spring` command will use these defaults:

```
$ spring init my-app
```

This will create a new Spring Boot application in the `~/projects/my-app` directory with a `com.example` package name.

We can also specify options on the `spring` command line. For example, we can use the `--project-dir` option to set the project directory:

```
$ spring init --project-dir=~/my-app my-app
```

This will create a new Spring Boot application in the `~/my-app` directory.

## Conclusion

In this post, we've looked at how to customize the Spring Boot CLI for advanced development. We've covered how to install the CLI, how to create and run Spring Boot applications, and how to customize the CLI for your own development needs.