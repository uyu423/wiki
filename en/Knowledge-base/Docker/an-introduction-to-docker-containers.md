---
title: An Introduction to Docker Containers
description: 
published: true
date: 2023-02-01T13:36:45.139Z
tags: 
editor: markdown
dateCreated: 2023-02-01T13:36:41.589Z
---

- [Docker 컨테이너 소개***Korean** version of this document is available*](/ko/Knowledge-base/Docker/an-introduction-to-docker-containers)
{.links-list}
- [Docker 容器简介***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Docker/an-introduction-to-docker-containers)
{.links-list}



# An Introduction to Docker Containers

In this article, we'll be discussing what Docker containers are, how they work, and some of the benefits they offer compared to other virtualization technologies.

## What are Docker Containers?

Docker containers are a type of virtualization technology that allow you to package and isolate an application with its dependencies, making it easy to deploy and run on any platform.

Unlike other virtualization technologies, such as virtual machines, Docker containers do not require a separate operating system for each application. This makes them much lighter weight and much faster to start up.

## How Do Docker Containers Work?

Docker containers work by using the Linux kernel's built-in support for namespaces and control groups (cgroups).

Namespaces allow you to isolate an application from the rest of the system, so that it appears as if it is the only application running on the system. This isolation is achieved by creating a separate set of resources, such as process IDs, network interfaces, and mount points, for the application.

Control groups (cgroups) allow you to limit the amount of resources, such as CPU and memory, that an application can use. This ensures that one application cannot hog all the resources and starve the others.

## Why Use Docker Containers?

There are many reasons why you might want to use Docker containers.

Docker containers are much lighter weight than virtual machines, so they start up much faster. This is important for development, where you might want to quickly spin up a new container to test something out.

Docker containers are also portable, so you can easily move them from one server to another. This is handy for production, where you might want to move an application to a different server for scaling or redundancy.

Another big benefit of Docker containers is that they allow you to isolate an application from the rest of the system. This is important for security, as it reduces the attack surface of the system.

## How to Use Docker Containers

Now that we've seen some of the benefits of Docker containers, let's look at how to use them.

The first thing you need is a Docker host. This is a Linux server with the Docker daemon installed. The daemon is the process that runs the containers.

You can install the Docker daemon on your own server, or you can use a service such as Amazon Elastic Container Service (ECS) or Google Container Engine (GKE).

Once you have a Docker host, you can start creating containers. Each container is created from a Docker image. An image is a template that contains the files and software needed to run an application.

There are two ways to get Docker images. The first is to create your own images, using a tool such as Dockerfile. The second is to use a public repository such as Docker Hub.

Once you have an image, you can use the Docker daemon to create a container from it. The Docker daemon will pull the image from the repository, create the container, and start the application.

You can then access the application by connecting to the Docker host. For example, if you are running a web application, you would connect to the host's IP address using a web browser.

## Conclusion

Docker containers are a type of virtualization technology that offer many benefits over other virtualization technologies, such as virtual machines.

Docker containers are much lighter weight, so they start up much faster. They are also portable, so you can easily move them from one server to another.

Another big benefit of Docker containers is that they allow you to isolate an application from the rest of the system. This is important for security, as it reduces the attack surface of the system.

If you are looking for a way to virtualize your applications, Docker containers are a great option.