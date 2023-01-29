---
title: Building a Kafka-based data pipeline with Spring Batch
description: Learn how to build a Kafka-based data pipeline with Spring Batch.
published: true
date: 2023-01-29T16:10:03.582Z
tags: batch framework, data pipeline, kafka, spring batch, streaming platform
editor: markdown
dateCreated: 2023-01-29T15:24:54.955Z
---

# Dockerizing your Node.js applications

Docker is a technology that allows you to package your applicationsinto a standardized unit for software development. Docker containers wrap up  a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries  – anything that can be installed on a server. This guarantees that it will always run the same, regardless of the environment it is running in.

Docker is ideal for Node.js applications because they are often designed to run in  simple environments and be packaged with only their dependencies. In most cases, you will want to package your Node.js applications into a  Docker container for easy distribution and development.

There are many ways to install and use Docker on your local development machine. In this article, we will show you how to install Docker  using the Homebrew package manager on macOS. We will also show you how to create a simple Node.js application and  package it into a Docker container.

## Installing Docker

Docker can be installed on your local development machine using the Homebrew package manager. Homebrew is a package manager for macOS that makes it easy to install and manage software on your computer.

To install Docker with Homebrew, first you need to install Homebrew. You can do this by running the following command in your terminal:

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once Homebrew is installed, you can install Docker by running the following command in your terminal:

```
$ brew install docker
```

After Docker is installed, you can verify that it is working by running the following command:

```
$ docker --version
```

You should see a message that looks like this:

```
Docker version 18.06.1-ce, build e68fc7a
```

## Creating a Node.js application

Now that you have Docker installed, let's create a simple Node.js application that we can package into a Docker container. Create a new directory for your project and change into that directory.

In your project directory, create a new file called `app.js` and add the following code:

```
const http = require('http');

const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World\n');
});

server.listen(port, () => {
  console.log(`Server is listening on port ${port}`);
});
```

This is a very simple Node.js application that creates an HTTP server and listens on port 3000. When a request is made to the server, it responds with "Hello, World".

## Packaging the Node.js application into a Docker container

Now that we have a simple Node.js application, let's package it into a Docker container. First, we need to create a file called `Dockerfile` in our project directory. A `Dockerfile` is a text file that contains all the commands that are needed to build a Docker image.

Add the following code to your `Dockerfile`:

```
FROM node:alpine

WORKDIR /usr/src/app

COPY app.js .

EXPOSE 3000

CMD ["node", "app.js"]
```

Let's break down each line of the `Dockerfile`:

- The `FROM` directive specifies the base image that we are going to use to build our image. In this case, we are using the `node:alpine` image.
- The `WORKDIR` directive sets the working directory for all subsequent commands. In this case, we are setting the working directory to `/usr/src/app`.
- The `COPY` directive copies the `app.js` file from our project directory into the working directory.
- The `EXPOSE` directive exposes port 3000 so that it can be accessed from outside the container.
- The `CMD` directive specifies the command that will be run when the container is started. In this case, we are running the `node` command with the `app.js` file.

Now that we have our `Dockerfile`, we can build our Docker image. To do this, run the following command in your terminal:

```
$ docker build -t node-app .
```

This will build a Docker image with the tag `node-app` from the `Dockerfile` in the current directory.

Once the image is built, we can run it as a container. To do this, run the following command:

```
$ docker run -p 3000:3000 node-app
```

This will start a container from the `node-app` image and expose port 3000 so that it can be accessed from outside the container.

You can now access your Node.js application by going to http://localhost:3000 in your web browser. You should see the message "Hello, World".

## Summary

In this article, we showed you how to install Docker and use it to package a Node.js application. Docker is a great tool for developing Node.js applications because it makes it easy to package your application with all of its dependencies. It also makes it easy to distribute your application to other developers or deploy it to production.