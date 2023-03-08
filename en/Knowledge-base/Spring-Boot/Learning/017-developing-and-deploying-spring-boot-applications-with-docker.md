---
title: 017: Developing and deploying Spring Boot applications with Docker
description: 
published: true
date: 2023-02-03T10:04:58.700Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:04:53.795Z
---

- [017: Desarrollo e implementación de aplicaciones Spring Boot con Docker***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/017-developing-and-deploying-spring-boot-applications-with-docker)
{.links-list}
- [017：使用 Docker 开发和部署 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/017-developing-and-deploying-spring-boot-applications-with-docker)
{.links-list}
- [017: Docker를 사용하여 Spring Boot 애플리케이션 개발 및 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/017-developing-and-deploying-spring-boot-applications-with-docker)
{.links-list}


# Developing and deploying Spring Boot applications with Docker

Docker is a tool that can greatly simplify the process of developing and deploying Spring Boot applications. In this post, we'll take a look at how to use Docker to develop and deploy a Spring Boot application.

## Developing a Spring Boot application with Docker

Developing a Spring Boot application with Docker is very simple. All you need is a text editor and a Dockerfile.

A Dockerfile is a text file that contains all the commands necessary to build a Docker image. A Docker image is a file that contains all the necessary files and dependencies for an application to run.

To create a Dockerfile, create a new file called `Dockerfile` in the root directory of your project. Then, add the following lines to the file:

```
FROM java:8

ADD . /app

WORKDIR /app

RUN ./gradlew build

EXPOSE 8080

CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]
```

The first line, `FROM java:8`, tells Docker to use the `java:8` Docker image as the base image for our application. The `java:8` Docker image contains all the necessary files and dependencies for a Java 8 application.

The second line, `ADD . /app`, tells Docker to add all the files in the current directory (`./`) to the `/app` directory in the Docker image.

The third line, `WORKDIR /app`, tells Docker to use the `/app` directory as the working directory for our application.

The fourth line, `RUN ./gradlew build`, tells Docker to run the `./gradlew build` command to build our application. This command will compile our code and create a `.jar` file in the `build/libs` directory.

The fifth line, `EXPOSE 8080`, tells Docker to expose port `8080` for our application.

The sixth and final line, `CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]`, tells Docker to run the `java` command with the `-jar` option and the `spring-boot-app-0.0.1-SNAPSHOT.jar` file as arguments. This will start our application on port `8080`.

Now that we have a Dockerfile, we can build a Docker image for our application. To do this, open a terminal and navigate to the root directory of your project. Then, run the following command:

```
$ docker build -t spring-boot-app .
```

This command will build a Docker image for our application and tag it with the `spring-boot-app` name.

Once the image is built, we can run it using the following command:

```
$ docker run -p 8080:8080 spring-boot-app
```

This command will start a Docker container for our image and map port `8080` on the host machine to port `8080` on the container.

Now, we can access our application at `http://localhost:8080`.

## Deploying a Spring Boot application with Docker

Deploying a Spring Boot application with Docker is just as simple as developing one. All we need is a Dockerfile and a docker-compose.yml file.

A docker-compose.yml file is a YAML file that contains all the necessary configuration for docker-compose, a tool that can be used to manage multi-container applications.

To create a docker-compose.yml file, create a new file called `docker-compose.yml` in the root directory of your project. Then, add the following lines to the file:

```
version: '2'

services:
  app:
    build: .
    ports:
      - "8080:8080"
```

The first line, `version: '2'`, tells docker-compose to use version 2 of the docker-compose file format.

The second line, `services:`, tells docker-compose that we are going to define a service. A service is a container that is part of a multi-container application.

The third line, `app:`, is the name of our service.

The fourth line, `build: .`, tells docker-compose to build our service using the `Dockerfile` in the current directory (`./`).

The fifth and final line, `ports: - "8080:8080"`, tells docker-compose to map port `8080` on the host machine to port `8080` on the container.

Now that we have a docker-compose.yml file, we can deploy our application using the following command:

```
$ docker-compose up
```

This command will start our application on port `8080`.

## Conclusion

In this post, we've seen how to use Docker to develop and deploy a Spring Boot application. Docker can greatly simplify the process of developing and deploying Spring Boot applications.