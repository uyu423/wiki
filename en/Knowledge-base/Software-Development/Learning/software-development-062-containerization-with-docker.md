---
title: Software Development 062: Containerization with Docker
description: 
published: true
date: 2023-02-28T04:32:16.851Z
tags: 
editor: markdown
dateCreated: 2023-02-28T04:32:15.452Z
---

- [소프트웨어 개발 062: Docker를 사용한 컨테이너화***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-062-containerization-with-docker)
{.links-list}


# Containerization with Docker

## What is containerization?

Containerization is a method of packaging and running applications where the application and its dependencies are isolated from the underlying host operating system. This isolation is achieved through the use of containers, which are similar to virtual machines in that they allow you to run an operating system within an operating system, but differ in that they are much lighter weight and share the kernel of the host operating system.

Docker is the most popular containerization platform and is what we will be using in this post.

## What is Docker?

Docker is a platform for developers and sysadmins to build, ship, and run distributed applications. It consists of a container runtime, a container orchestration tool, and a registry for storing and sharing container images.

Docker containers are isolated from each other and from the host operating system, but they share the kernel of the host operating system. This makes them much lighter weight than virtual machines.

Docker is available on Windows, macOS, and Linux.

## How to use Docker

Docker is used to run containers. A container is a self-contained environment that includes the application and all of its dependencies.

To use Docker, you first need to install it. You can find installation instructions for your platform here:

https://docs.docker.com/install/

Once Docker is installed, you can pull images from the Docker Hub, which is a registry of Docker images. To pull an image, use the ```docker pull``` command. For example, to pull the latest version of the Ubuntu image, you would use the following command:

```
docker pull ubuntu
```

You can also run containers from images that you have built yourself. To build an image, you need a ```Dockerfile```, which is a text file that contains instructions for how to build the image.

Once you have a Dockerfile, you can use the ```docker build``` command to build the image. For example, the following command would build an image from the Dockerfile in the current directory:

```
docker build -t myimage:latest .
```

Once you have built an image, you can use the ```docker run``` command to run a container from the image. For example, the following command would run a container from the image we just built:

```
docker run -it myimage:latest
```

This would run the container in interactive mode (-it), which allows you to interact with the container. If you just want to run the container in the background, you can use the -d option instead of -it.

## Conclusion

In this post, we have covered what containerization is and how to use Docker to run containers. Containerization is a great way to package and run applications in a self-contained environment that is isolated from the host operating system. Docker is the most popular containerization platform and is available on Windows, macOS, and Linux.