---
title: 028: Building and deploying a Spring Boot application to PaaS (Heroku, OpenShift)
description: 
published: true
date: 2023-02-03T20:32:40.854Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:32:39.166Z
---

- [028: Creación e implementación de una aplicación Spring Boot para PaaS (Heroku, OpenShift)***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/028-building-and-deploying-a-spring-boot-application-to-paas-heroku-openshift)
{.links-list}
- [028：构建 Spring Boot 应用程序并将其部署到 PaaS（Heroku、OpenShift）***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/028-building-and-deploying-a-spring-boot-application-to-paas-heroku-openshift)
{.links-list}
- [028: PaaS(Heroku, OpenShift)에 Spring Boot 애플리케이션 구축 및 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/028-building-and-deploying-a-spring-boot-application-to-paas-heroku-openshift)
{.links-list}


# 028: Building and deploying a Spring Boot application to PaaS (Heroku, OpenShift)

In this post, we'll learn how to build and deploy a Spring Boot application to a Platform as a Service (PaaS) provider. In particular, we'll focus on two popular PaaS providers, Heroku and OpenShift.

Building and deploying Spring Boot applications to PaaS providers is a great way to get your application up and running quickly. PaaS providers handle all of the infrastructure and deployment configuration for you, so you can focus on developing your application.

## Prerequisites

Before we get started, there are a few things you'll need:

* A PaaS account. You can sign up for a free Heroku account at [heroku.com](https://www.heroku.com/). For OpenShift, you can sign up for a free account at [openshift.com](https://www.openshift.com/).
* A text editor or IDE. We'll be using [Visual Studio Code](https://code.visualstudio.com/) in this post, but you can use any editor you like.
* [JDK 8](https://adoptopenjdk.net/) or later.
* [Maven](https://maven.apache.org/) 3.3.9 or later.

## Creating a Spring Boot application

Let's start by creating a simple Spring Boot application. We'll use the [Spring Initializr](https://start.spring.io/) to generate the project.

Go to the [Spring Initializr](https://start.spring.io/) and select the following options:

* Generate a `Maven Project`
* Use `Java 8`
* Use `Spring Boot 2.2.2`
* Packaging: `Jar`
* Type: `Web`
* Artifact: `demo`

Click `Generate Project`, and a `demo.zip` file will be downloaded. Extract the contents of the zip file to a directory on your computer.

Open the project in Visual Studio Code, and you should see the following project structure:

```
demo
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── demo
        │               └── DemoApplication.java
        └── resources
            └── application.properties
```

The `pom.xml` file is the Maven project configuration file. The `src/main/java` directory contains the Java source code for the application. The `src/main/resources` directory contains application configuration files.

Open the `DemoApplication.java` file and add the following `@RestController`:

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoApplication {

    @GetMapping("/")
    public String home() {
        return "Hello, world!";
    }

}
```

This `@RestController` exposes a `/` endpoint that returns the `Hello, world!` string.

## Running the application locally

Let's run the application locally to make sure it works. In the terminal, navigate to the `demo` directory and run the following command:

```
mvn spring-boot:run
```

This will start the application on your local machine. You can access the application at [http://localhost:8080](http://localhost:8080). You should see the `Hello, world!` string.

## Deploying the application to Heroku

Now that we have a working application, let's deploy it to Heroku.

Heroku uses [Git](https://git-scm.com/) for deployment, so the first thing we need to do is initialize a Git repository in the `demo` directory. In the terminal, run the following commands:

```
git init
git add .
git commit -m "Initial commit"
```

This will initialize a Git repository and make the initial commit.

Next, we need to create a Heroku application. In the terminal, run the following command:

```
heroku create
```

This will create a new Heroku application and add a remote to your Git repository.

Now we can deploy the application to Heroku. In the terminal, run the following command:

```
git push heroku master
```

This will push the code to the Heroku remote and trigger a deployment.

Once the deployment is complete, you can view the application at the URL provided by Heroku. You should see the `Hello, world!` string.

## Deploying the application to OpenShift

OpenShift uses [Git](https://git-scm.com/) for deployment, so the first thing we need to do is initialize a Git repository in the `demo` directory. In the terminal, run the following commands:

```
git init
git add .
git commit -m "Initial commit"
```

This will initialize a Git repository and make the initial commit.

Next, we need to create a new OpenShift project. An OpenShift project is a logical grouping of resources. We'll use the OpenShift web console to create the project.

Log in to the [OpenShift web console](https://console.openshift.com/) and click `Create Project`. Enter `demo` for the project name and click `Create`.

Once the project has been created, we can deploy the application to OpenShift. In the terminal, run the following command:

```
git push openshift master
```

This will push the code to the OpenShift remote and trigger a deployment.

Once the deployment is complete, you can view the application at the URL provided by OpenShift. You should see the `Hello, world!` string.