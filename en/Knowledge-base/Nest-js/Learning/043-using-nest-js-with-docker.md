---
title: 043: Using Nest.js with Docker
description: 
published: true
date: 2023-02-15T14:32:57.673Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:32:50.213Z
---

- [043: Uso de Nest.js con Docker***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/043-using-nest-js-with-docker)
{.links-list}
- [043：将 Nest.js 与 Docker 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/043-using-nest-js-with-docker)
{.links-list}
- [043: Nest.js를 도커와 함께 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/043-using-nest-js-with-docker)
{.links-list}


# Using Nest.js with Docker

Docker is a great tool for developing and deploying web applications. It allows you to package your application into a self-contained environment that is easy to deploy and manage.

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (which brings static type-checking to JavaScript) and combines elements of both Object-Oriented Programming and Functional Programming.

In this post, we'll learn how to use Nest.js with Docker. We'll start by creating a simple Nest.js application and then containerize it using Docker. We'll also learn how to use Docker Compose to manage our application's dependencies.

## Creating a Nest.js Application

Let's start by creating a simple Nest.js application. We'll call our application "todo-list."

First, we need to install the Nest.js CLI. We can do this using npm:

```
npm install -g @nestjs/cli
```

Once the Nest.js CLI is installed, we can create our application using the following command:

```
nest new todo-list
```

This will create a new directory called "todo-list" and generate the basic scaffolding for our Nest.js application.

Next, we need to install the dependencies for our application. We can do this using npm:

```
cd todo-list
npm install
```

Now that our application's dependencies are installed, we can start the application using the following command:

```
npm start
```

This will start the application on port 3000. We can view the application in our browser by navigating to http://localhost:3000.

## Containerizing our Application

Now that we have a basic Nest.js application up and running, let's containerize it using Docker.

First, we need to create a file called "Dockerfile" in the root directory of our application. This file will contain the instructions for building our Docker image.

Our Dockerfile will start with the following line:

```
FROM node:10-alpine
```

This line specifies that we want to use the Node.js 10 Alpine image as the base image for our Docker image. Alpine is a lightweight Linux distribution that is perfect for using as a base image for our application.

Next, we need to copy the files for our application into the image. We can do this using the COPY command:

```
COPY . .
```

This will copy all of the files in the current directory into the image.

Now that our files are copied, we need to install our application's dependencies. We can do this using the npm command:

```
RUN npm install
```

Finally, we need to specify the command that will be used to start our application. We can do this using the CMD command:

```
CMD ["npm", "start"]
```

This will start our application when the container is started.

Our Dockerfile is now complete. We can build our Docker image using the following command:

```
docker build -t todo-list .
```

This will build an image called "todo-list" using the instructions in our Dockerfile.

Once our image is built, we can run it using the following command:

```
docker run -d -p 3000:3000 todo-list
```

This will start a container based on our "todo-list" image and map port 3000 on the container to port 3000 on our host machine.

We can now view our application in our browser by navigating to http://localhost:3000.

## Using Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to specify the dependencies for your application in a single file and then start all of the containers with a single command.

Let's create a "docker-compose.yml" file in the root directory of our application. This file will contain the instructions for running our application using Docker Compose.

Our docker-compose.yml file will start with the following line:

```
version: '3'
```

This line specifies that we are using version 3 of the Docker Compose file format.

Next, we need to specify the services that our application depends on. We can do this using the "services" key:

```
services:
  todo-list:
    image: todo-list
    ports:
      - "3000:3000"
```

This defines a service called "todo-list" that uses the "todo-list" image and maps port 3000 on the container to port 3000 on our host machine.

Now that our docker-compose.yml file is complete, we can start our application using the following command:

```
docker-compose up
```

This will start all of the containers defined in our docker-compose.yml file.

We can now view our application in our browser by navigating to http://localhost:3000.

## Conclusion

In this post, we learned how to use Nest.js with Docker. We started by creating a simple Nest.js application and then containerized it using Docker. We also learned how to use Docker Compose to manage our application's dependencies.