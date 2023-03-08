---
title: 077: Deploying a Spring Boot Application with Docker
description: 
published: true
date: 2023-02-05T08:32:57.605Z
tags: 
editor: markdown
dateCreated: 2023-02-05T08:32:52.067Z
---

- [077: Implementación de una aplicación Spring Boot con Docker***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/077-deploying-a-spring-boot-application-with-docker)
{.links-list}
- [077：使用 Docker 部署 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/077-deploying-a-spring-boot-application-with-docker)
{.links-list}
- [077: Docker를 사용하여 Spring Boot 애플리케이션 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/077-deploying-a-spring-boot-application-with-docker)
{.links-list}


## Introduction

Docker is a containerization technology that enables you to package an application with all its dependencies and ship it as one unit. This makes it easy to deploy and run your application on any host that supports Docker.

In this post, we'll learn how to deploy a Spring Boot application with Docker. We'll start by building a simple Spring Boot application and packaging it as a Docker image. Then we'll run the Docker image on a local Docker host. Finally, we'll push the Docker image to a Docker registry so it can be deployed on a production server.

## Prerequisites

To follow along with this post, you'll need the following:

- A text editor
- JDK 8 or later
- Maven 3.0 or later
- Docker CE 18.03 or later

## Building a Spring Boot application

We'll start by building a simple Spring Boot application. The application will have a single REST endpoint that returns a list of countries.

First, create a new directory for the project and change into that directory. Then create a file named `pom.xml` with the following contents:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-docker-example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

This is the Maven `pom.xml` file for the project. We're using the Spring Boot starter parent, which provides a convenient way to manage dependencies and configure the build. We're also using the Spring Boot starter web dependency, which includes the dependencies for building a web application.

Next, create a file named `src/main/java/com/example/springboot/Application.java` with the following contents:

```java
package com.example.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

This is the main application class. It uses the `@SpringBootApplication` annotation to enable auto-configuration and component scanning.

Next, create a file named `src/main/java/com/example/springboot/controller/CountryController.java` with the following contents:

```java
package com.example.springboot.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
public class CountryController {

    @GetMapping("/countries")
    public List<String> getCountries() {
        return Arrays.asList("Australia", "Canada", "France", "Germany", "India", "Japan", "United Kingdom", "United States");
    }

}
```

This is the controller for the `/countries` endpoint. It returns a list of countries.

Now that the application is complete, we can package it as a Docker image.

## Packaging the application as a Docker image

We'll use Maven to package the application as a Docker image. First, we need to add a `<plugin>` to the `pom.xml` file:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.repository}</repository>
                <tag>${project.version}</tag>
                <buildArgs>
                    <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
                </buildArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```

This adds the Spotify Dockerfile Maven plugin, which will package the application as a Docker image. We're also configuring the plugin to use the `${project.version}` as the Docker image tag and to pass the `${project.build.finalName}.jar` file as a build argument.

Next, create a file named `src/main/docker/Dockerfile` with the following contents:

```dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

This is the Dockerfile for the image. It uses the OpenJDK 8 Alpine Docker image as the base image. It also copies the `${JAR_FILE}` to the `app.jar` file and sets it as the entrypoint for the image.

Now we can package the application as a Docker image by running the following command:

```
$ mvn package docker:build
```

This will package the application as a JAR file and build a Docker image. The Docker image will be tagged with the `${project.version}`, which in this case is `1.0-SNAPSHOT`.

## Running the Docker image

Now that we have a Docker image, we can run it on a local Docker host. First, we need to start a Docker host. If you're using Docker Machine, you can start a Docker host with the following command:

```
$ docker-machine create --driver virtualbox default
```

This will create a Docker host with the name `default`.

Next, we need to set some environment variables so we can access the Docker host:

```
$ eval $(docker-machine env default)
```

Now we can run the Docker image with the following command:

```
$ docker run -d -p 8080:8080 spring-boot-docker-example:1.0-SNAPSHOT
```

This will run the Docker image in detached mode and map port `8080` on the Docker host to port `8080` on the container.

You can verify that the container is running with the following command:

```
$ docker ps
```

You should see an output like this:

```
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
e9c4b7a4d4f4        spring-boot-docker-example:1.0   "java -Djava.securit…"   3 seconds ago       Up 2 seconds        0.0.0.0:8080->8080/tcp   stoic_ardinghelli
```

Now we can access the application by opening http://localhost:8080 in a web browser. You should see a page like this:

![Spring Boot Docker Example](https://i.imgur.com/hm4Tv0b.png)

## Pushing the Docker image to a registry

Now that we have a working Docker image, we can push it to a Docker registry so it can be deployed on a production server.

First, we need to create a Docker registry. We'll use the Docker Hub for this example. Sign up for a Docker Hub account and then create a new repository. We'll call our repository `spring-boot-docker-example`.

Once the repository has been created, we can push our Docker image to it with the following command:

```
$ docker push spring-boot-docker-example:1.0-SNAPSHOT
```

This will push the `spring-boot-docker-example:1.0-SNAPSHOT` image to the `spring-boot-docker-example` repository on Docker Hub.

## Conclusion

In this post, we learned how to deploy a Spring Boot application with Docker. We started by building a simple Spring Boot application and packaging it as a Docker image. Then we ran the Docker image on a local Docker host. Finally, we pushed the Docker image to a Docker registry so it could be deployed on a production server.