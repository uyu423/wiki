---
title: Dockerfile Best Practices: Creating Reliable Docker Images
description: 
published: true
date: 2023-02-15T23:32:54.907Z
tags: 
editor: markdown
dateCreated: 2023-02-15T23:32:47.224Z
---

- [Prácticas recomendadas de Dockerfile: creación de imágenes de Docker fiables***Spanish** document is available*](/es/Knowledge-base/Docker/dockerfile-best-practices-creating-reliable-docker-images)
{.links-list}
- [Dockerfile 最佳实践：创建可靠的 Docker 镜像***Chinese Simplified** document is available*](/zh/Knowledge-base/Docker/dockerfile-best-practices-creating-reliable-docker-images)
{.links-list}
- [Dockerfile 모범 사례: 신뢰할 수 있는 Docker 이미지 생성***Korean** document is available*](/ko/Knowledge-base/Docker/dockerfile-best-practices-creating-reliable-docker-images)
{.links-list}


# Dockerfile Best Practices: Creating Reliable Docker Images

Dockerfiles are a fundamental part of using Docker. They allow you to create your own images, which can be used to create new containers. A well-crafted Dockerfile can make it easy to create, maintain and update your images, and can save you a lot of time and effort in the long run.

This article will offer some best practices for creating reliable Docker images, with the aim of making your life easier as a Docker user.

## Use .dockerignore

The .dockerignore file is used to specify files and directories which should be excluded from your image. This is useful for excluding files which are not needed in your image, such as temporary files or build artifacts.

To create a .dockerignore file, simply create a file named ".dockerignore" in your project's root directory, and add each file or directory you wish to exclude, one per line. For example:

```
.dockerignore

# Exclude all temporary files
*.tmp

# Exclude all build artifacts
build/
```

## Keep your Dockerfile simple

A simple Dockerfile is easier to understand and maintain than a complex one. It is also more likely to be compatible with future versions of Docker.

One way to keep your Dockerfile simple is to avoid using complex shell commands. If possible, use existing docker images as a base for your own image, and install the necessary software using a package manager such as apt or yum.

Another way to keep your Dockerfile simple is to avoid installing unnecessary software. If you are only using a image for a specific purpose, there is no need to install a full operating system with a text editor, web browser, etc.

## Use a specific tag for your base image

When using a base image from a Docker registry, always specify a specific tag rather than using the "latest" tag. The "latest" tag is often used by developers to indicate the most recent development version of an image, which might not be suitable for production use.

## Use a single RUN instruction

If possible, use a single RUN instruction in your Dockerfile rather than multiple instructions. This will make your image easier to build and will reduce the number of layers in your image, which can be important for performance.

To use a single RUN instruction, simply combine all the commands you wish to run into a single line, separated by &&. For example:

```
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:my-ppa && \
    apt-get update && \
    apt-get install -y my-software
```

## Use a specific user

By default, containers run as the root user. This can be a security risk, as any processes running in the container will have full access to the host machine.

To avoid this, you can create a new user in your Dockerfile and use this user for running any processes in the container. For example:

```
# Create a new user
RUN useradd -ms /bin/bash myuser

# Use the new user for all subsequent commands
USER myuser
```

## Use a specific working directory

When a container is created, it is given a default working directory. This directory can be overridden using the WORKDIR instruction in your Dockerfile.

It is a good idea to specify a specific working directory, as it can make it easier to find files in your container and can help with portability between different machines. For example:

```
# Set the working directory to /app
WORKDIR /app
```

## Avoid using ADD and COPY

The ADD and COPY instructions are similar, but there are some important differences between them. ADD can be used to extract files from a remote URL, whereas COPY can only be used to copy files from the build context.

ADD is also more powerful than COPY, as it can automatically resolve dependencies between files. For example, if you ADD a .tar.gz file, ADD will automatically extract the files from the archive.

Due to these differences, it is generally recommended to use COPY rather than ADD in your Dockerfile.

## Specify a health check

A health check is a test which is used to determine whether a container is healthy and should continue running. If a health check fails, the container will be stopped and restarted.

Health checks can be specified using the HEALTHCHECK instruction in your Dockerfile. For example:

```
# Check that the container is healthy every 30 seconds
# and that the HTTP service is responding on port 80
HEALTHCHECK --interval=30s --timeout=5s \
    CMD wget -qO- http://localhost:80/ || exit 1
```

## Use multi-stage builds

Multi-stage builds are a feature of Docker which allows you to create multiple images as part of a single build process. This can be useful for creating images which are smaller and more secure, as you can remove unnecessary files from your image after building it.

To use multi-stage builds, simply create multiple FROM instructions in your Dockerfile, each with a different image name. For example:

```
# Build stage
FROM golang:1.8 as builder

WORKDIR /src

COPY . .

RUN go build -o app

# Run stage
FROM alpine:latest

WORKDIR /app

COPY --from=builder /src/app .

CMD ["./app"]
```

## Conclusion

By following the best practices described in this article, you can make your Dockerfiles more reliable, easier to understand and easier to maintain. This will save you time and effort in the long run, and will make your life as a Docker user much easier.