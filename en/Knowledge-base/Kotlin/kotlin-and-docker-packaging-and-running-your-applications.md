---
title: Kotlin and Docker: Packaging and Running Your Applications
description: 
published: true
date: 2023-02-12T00:17:35.969Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:17:29.384Z
---

- [Kotlin y Docker: empaquetado y ejecución de sus aplicaciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/kotlin-and-docker-packaging-and-running-your-applications)
{.links-list}
- [Kotlin 和 Docker：打包和运行您的应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-docker-packaging-and-running-your-applications)
{.links-list}
- [Kotlin 및 Docker: 애플리케이션 패키징 및 실행***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-docker-packaging-and-running-your-applications)
{.links-list}


# Kotlin and Docker: Packaging and Running Your Applications

Kotlin is a JVM-compatible language that has gained popularity in recent years for its concise syntax and interoperability with Java. Docker is a containerization platform that enables developers to package and run applications in isolated environments.

In this article, we will show how to package a Kotlin application into a Docker container and run it on a server. We will also briefly discuss some of the benefits of using Kotlin and Docker together.

## Packaging a Kotlin Application in a Docker Container

To package a Kotlin application in a Docker container, we need to create a `Dockerfile` that specifies the base image and the necessary dependencies. We will use the `openjdk:8-jdk-alpine` image as our base image. This image contains the OpenJDK 8 JVM and the Alpine Linux distribution. Alpine Linux is a lightweight Linux distribution that is ideal for Docker containers.

We will also need to specify the `kotlin-stdlib` dependency. This dependency contains the Kotlin standard library, which is required for all Kotlin applications.

```Dockerfile
FROM openjdk:8-jdk-alpine

# Add the Kotlin standard library as a dependency
RUN apk add --no-cache kotlin-stdlib
```

Next, we need to copy our Kotlin code into the container. We will place our code in the `/app` directory.

```Dockerfile
# Copy our Kotlin code into the container
COPY src/ /app/src/
```

Finally, we need to specify the `ENTRYPOINT` and `CMD` values. The `ENTRYPOINT` value specifies the command that will be run when the container is started. The `CMD` value specifies the arguments that will be passed to the `ENTRYPOINT` command. In our case, we will use the `kotlinc` command to compile our code and the `java` command to run our compiled code.

```Dockerfile
# Specify the entrypoint and command
ENTRYPOINT ["kotlinc", "-include-runtime", "/app/src/main.kt", "-d", "/app/app.jar"]
CMD ["java", "-jar", "/app/app.jar"]
```

The `-include-runtime` argument tells the `kotlinc` compiler to include the Kotlin runtime in the compiled code. This is necessary because the Kotlin runtime is not included in the `kotlin-stdlib` dependency.

## Running a Kotlin Application in a Docker Container

Now that we have our `Dockerfile`, we can build our Docker image and run our Kotlin application in a Docker container.

First, we need to build our Docker image. We will use the `docker build` command to build our image. We will name our image `kotlin-app` and tag it with the `latest` tag.

```console
$ docker build -t kotlin-app:latest .
```

Next, we need to run our Docker image. We will use the `docker run` command to run our image. We will also specify the `-p 8080:8080` argument, which will map port `8080` on the host to port `8080` in the container.

```console
$ docker run -p 8080:8080 kotlin-app:latest
```

Our Kotlin application is now running in a Docker container and can be accessed at `http://localhost:8080`.

## Benefits of Using Kotlin and Docker Together

There are several benefits to using Kotlin and Docker together.

First, Kotlin is a very concise language. This means that our Kotlin code will be much smaller than the equivalent Java code. This is important when packaging applications in Docker containers because smaller images are faster to build and deploy.

Second, Kotlin is fully interoperable with Java. This means that we can easily use existing Java libraries in our Kotlin code. This is important when containerizing existing Java applications with Docker.

Third, Kotlin is a JVM-compatible language. This means that we can run our Kotlin code on any platform that supports the JVM. This is important when deploying applications in Docker containers because we can run our containers on any platform that supports Docker, regardless of the underlying operating system.

## Conclusion

In this article, we showed how to package a Kotlin application in a Docker container and run it on a server. We also briefly discussed some of the benefits of using Kotlin and Docker together.