---
title: Linux Containerization with Docker
description: 
published: true
date: 2023-02-12T02:32:27.031Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:32:20.494Z
---

- [Contenedorización de Linux con Docker***Spanish** document is available*](/es/Knowledge-base/Linux/linux-containerization-with-docker)
{.links-list}
- [使用 Docker 进行 Linux 容器化***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-containerization-with-docker)
{.links-list}
- [Docker를 사용한 Linux 컨테이너화***Korean** document is available*](/ko/Knowledge-base/Linux/linux-containerization-with-docker)
{.links-list}


# Linux Containerization with Docker

In this article, we'll be looking at Linux containerization with Docker. We'll cover what containers are, how they work, and why you might want to use them. We'll also go over some basic commands for working with Docker containers. By the end of this article, you should have a good understanding of how to use Docker to containerize your applications.

## What are containers?

Containers are a way of isolating your application from the rest of the system. They work by packaging up the application and its dependencies into a single unit that can be run anywhere. This isolation makes it much easier to move your application around and ensures that it will always run the same, no matter where it's deployed.

## How do containers work?

Containers are built on top of a Linux kernel feature called namespaces. Namespaces allow you to create isolated environments within a single Linux system. This isolation is what allows you to run multiple containers on a single host.

Each container has its own set of namespaces, which provides it with its own isolated environment. This environment includes its own process tree, network interfaces, mount points, and more. This isolation means that a containerized application will always run the same, no matter where it's deployed.

## Why use containers?

There are a few reasons you might want to use containers.

### 1. Portability

Containers are portable, meaning they can be easily moved from one system to another. This makes it easy to deploy your applications on multiple platforms.

### 2. Reproducibility

Containers are also reproducible, meaning that they can be easily recreated. This is important for development and testing, as you can always be sure that your application will run the same in production as it does in your development environment.

### 3. Resource isolation

Containers provide resource isolation, meaning that each container has its own isolated environment. This isolation ensures that your application will always have the resources it needs to run, regardless of what other applications are running on the same system.

## Getting started with Docker

Now that we've covered what containers are and why you might want to use them, let's take a look at how to use Docker to containerize your applications.

Docker is a tool that makes it easy to work with containers. It provides a command-line interface for managing containers, as well as a platform for sharing container images.

### Installing Docker

Before you can use Docker, you'll need to install it on your system. Docker is available for a variety of platforms, including Linux, macOS, and Windows.

To install Docker on Ubuntu, you can use the following command:

```
sudo apt-get install docker.io
```

Once Docker is installed, you can use the `docker` command to manage containers.

### Creating a container

To create a container, you can use the `docker run` command. This command takes a container image and creates a new container from it. For example, to create a container from the Ubuntu image, you can use the following command:

```
docker run -it ubuntu
```

This command will pull the Ubuntu image from Docker Hub and create a new container from it. The `-it` flag tells Docker to run the container in interactive mode.

Once the container is running, you'll be placed into a Bash shell inside the container. From here, you can run any commands you like. When you're finished, you can exit the container by typing `exit`.

### Viewing containers

To view a list of all the containers on your system, you can use the `docker ps` command. This command will show you the containers that are currently running, as well as the containers that have been created but are not running.

To view all containers, including those that have been created but are not running, you can use the `-a` flag.

### Starting and stopping containers

To start a container that is not currently running, you can use the `docker start` command. For example, to start the container we created in the previous section, you can use the following command:

```
docker start ubuntu
```

To stop a container that is currently running, you can use the `docker stop` command. For example, to stop the container we created in the previous section, you can use the following command:

```
docker stop ubuntu
```

### Deleting containers

To delete a container, you can use the `docker rm` command. For example, to delete the container we created in the previous section, you can use the following command:

```
docker rm ubuntu
```

## Conclusion

In this article, we've looked at what containers are and how to use Docker to containerize your applications. We've also covered some basic commands for working with Docker containers. By the end of this article, you should have a good understanding of how to use Docker to containerize your applications.