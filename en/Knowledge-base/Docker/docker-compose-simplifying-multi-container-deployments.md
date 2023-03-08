---
title: Docker Compose: Simplifying Multi-Container Deployments
description: 
published: true
date: 2023-02-01T12:57:39.505Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:57:38.042Z
---

- [Docker Compose: 다중 컨테이너 배포 간소화***Korean** version of this document is available*](/ko/Knowledge-base/Docker/docker-compose-simplifying-multi-container-deployments)
{.links-list}
- [Docker Compose：简化多容器部署***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Docker/docker-compose-simplifying-multi-container-deployments)
{.links-list}



# Docker Compose: Simplifying Multi-Container Deployments

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

Using Compose is basically a three-step process.

1. Define your app’s environment with a Dockerfile so it can be reproduced anywhere.

2. Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.

3. Run docker-compose up and Compose starts and runs your entire app.

## Define your app’s environment with a Dockerfile

A Dockerfile is a text document that contains all the commands you would normally execute manually in order to build a Docker image.

```
FROM node:8

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]
```

The first thing you need to do is specify which base image you want to use for your container. In this case we’re using node:8, which is a popular image for running Node.js applications.

Next, the WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.

The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the image at the path <dest>.

The RUN instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile.

In this case, we’re running npm install which will install all the dependencies defined in our package.json file.

The COPY . . instruction will copy all the files in our current directory into the container.

The EXPOSE instruction informs Docker that the container will listen on the specified network port at runtime.

The CMD instruction has two forms. The exec form, which is the preferred form, and the shell form.

The exec form makes it possible to avoid shell string munging, and to use different shells, or no shell at all. This prevents any CMD or RUN instruction that uses a shell form from being executed.

In this case we’re using the exec form and we’re specifying that when the container starts, it should execute the npm start command.

## Define the services that make up your app in docker-compose.yml

Now that we have our Dockerfile, we can define our services in a docker-compose.yml file.

```
version: '3'

services:
  web:
    build: .
    ports:
     - "8080:8080"
```

In this file, we’re defining a single service named web. This service is built using the Dockerfile in our current directory. And we’re mapping port 8080 on our host to port 8080 in our container.

## Run docker-compose up and Compose starts and runs your entire app

Now that we have our Dockerfile and docker-compose.yml file, we can start our app by running docker-compose up.

```
$ docker-compose up
```

This command will start our web service and print the logs to the console.

## Conclusion

Docker Compose is a great tool for simplifying the process of deploying multi-container Docker applications. By using a Dockerfile and docker-compose.yml file, you can define and run your entire app with a single command.