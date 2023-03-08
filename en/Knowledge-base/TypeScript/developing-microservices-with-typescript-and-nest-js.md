---
title: Developing Microservices with TypeScript and Nest.js
description: 
published: true
date: 2023-03-01T03:32:38.802Z
tags: 
editor: markdown
dateCreated: 2023-03-01T03:32:37.076Z
---

- [TypeScript 및 Nest.js로 마이크로서비스 개발***Korean** document is available*](/ko/Knowledge-base/TypeScript/developing-microservices-with-typescript-and-nest-js)
{.links-list}


# Developing Microservices with TypeScript and Nest.js

TypeScript is a powerful language that provides static type-checking along with features like classes, interfaces, and modules, to JavaScript development. Nest.js is a Node.js framework for building efficient, scalable, and enterprise-grade server-side applications. 

In this article, we'll explore how to develop a microservice using TypeScript and Nest.js. We'll start by looking at the benefits of using TypeScript and Nest.js for microservices. We'll then create a simple microservice using TypeScript and Nest.js. Finally, we'll deploy our microservice to a server.

## Benefits of Using TypeScript and Nest.js for Microservices

There are many benefits to using TypeScript and Nest.js for developing microservices. TypeScript provides static type-checking, which can help catch errors early in the development process. TypeScript's ability to import other TypeScript files means that you can easily modularize your code. Nest.js is built on top of TypeScript and shares many of its benefits. In addition, Nest.js provides a powerful module system that can help you organize your code. 

Nest.js also provides a number of features that are helpful for developing microservices. Nest.js is designed to be scalable and easy to use. It also supports a number of features that are helpful for microservices, such as message queues and databases.

## Creating a Simple Microservice

Now that we've looked at the benefits of using TypeScript and Nest.js for developing microservices, let's create a simple microservice. We'll start by creating a file called `main.ts` in our project directory. In `main.ts`, we'll import the `@nestjs/common` module and the `@nestjs/microservices` module. We'll also create a class called `Main` and decorate it with the `@nestjs/common` `@Controller` decorator.

```typescript
import { Controller, Get } from '@nestjs/common';
import { MessagePattern } from '@nestjs/microservices';

@Controller()
export class Main {

  @MessagePattern('add')
  add(data: number[]) {
    return data.reduce((a, b) => a + b);
  }
}
```

In the `Main` class, we've created a method called `add` that is decorated with the `@nestjs/microservices` `@MessagePattern` decorator. The `@MessagePattern` decorator tells Nest.js that this method should be invoked when a message with the pattern `add` is received. The `add` method takes an array of numbers as input and returns the sum of the numbers. 

Next, we'll create a file called `server.ts` in our project directory. In `server.ts`, we'll import the `@nestjs/microservices` module and the `Main` class. We'll also create a class called `Server` and decorate it with the `@nestjs/microservices` `@Microservice` decorator.

```typescript
import { Microservice } from '@nestjs/microservices';

import { Main } from './main';

@Microservice()
export class Server {
  constructor(private readonly main: Main) {}
}
```

In the `Server` class, we've injected an instance of the `Main` class using the `@nestjs/microservices` `@Inject` decorator. We've also decorated the `Server` class with the `@nestjs/microservices` `@Microservice` decorator. The `@Microservice` decorator tells Nest.js that this class is a microservice. 

Finally, we'll create a file called `package.json` in our project directory. In `package.json`, we'll add a script called `start` that will start our microservice.

```json
{
  "name": "my-microservice",
  "version": "1.0.0",
  "scripts": {
    "start": "nest start"
  },
  "dependencies": {
    "@nestjs/common": "^5.4.0",
    "@nestjs/microservices": "^5.4.0"
  }
}
```

## Deploying Our Microservice

Now that we've created our microservice, let's deploy it to a server. We'll use [Docker](https://www.docker.com/) to package our microservice into a container. We'll then use [docker-compose](https://docs.docker.com/compose/) to deploy our container to a server. 

First, we'll create a file called `Dockerfile` in our project directory. In `Dockerfile`, we'll use the [`node:10-alpine`](https://hub.docker.com/_/node/) Docker image and specify that our microservice should be run on port `3000`. We'll also copy the files from our project directory into the container and install our dependencies. 

```Dockerfile
FROM node:10-alpine

WORKDIR /usr/src/app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```

Next, we'll create a file called `docker-compose.yml` in our project directory. In `docker-compose.yml`, we'll specify that we want to use the `Dockerfile` we created and that we want to expose port `3000`.

```yaml
version: '3'

services:
  my-microservice:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
```

Now that we have our `Dockerfile` and `docker-compose.yml` files, we can deploy our microservice to a server. We'll use the [AWS Elastic Container Service (ECS)](https://aws.amazon.com/ecs/) to deploy our container to AWS. 

First, we'll create a file called `ecs-params.yml` in our project directory. In `ecs-params.yml`, we'll specify the name of our container, the port that our container will be exposed on, and the amount of memory and CPU that our container can use. 

```yaml
version: 1
task_definition:
  task_execution_role:
    Ref: EcsTaskExecutionRole
  container_definitions:
    - name: my-microservice
      image: my-microservice
      portMappings:
        - containerPort: 3000
          hostPort: 3000
      memory: 512
      cpu: 256
```

Now that we have our `ecs-params.yml` file, we can create our task definition. We'll create a file called `ecs-task-definition.json` in our project directory. In `ecs-task-definition.json`, we'll specify the name of our task definition, the IAM role that our task will use, and the container definition that we created in `ecs-params.yml`. 

```json
{
  "family": "my-microservice-task-definition",
  "executionRoleArn": "arn:aws:iam::123456789012:role/ecsTaskExecutionRole",
  "containerDefinitions": [
    {
      "name": "my-microservice",
      "image": "my-microservice",
      "portMappings": [
        {
          "containerPort": 3000,
          "hostPort": 3000
        }
      ],
      "memory": 512,
      "cpu": 256
    }
  ]
}
```

Now that we have our task definition, we can register our task definition with ECS. We'll create a file called `ecs-register-task-definition.json` in our project directory. In `ecs-register-task-definition.json`, we'll specify the name of our task definition and the `ecs-task-definition.json` file that we created. 

```json
{
  "taskDefinition": "my-microservice-task-definition",
  "cliInputJson": "file://ecs-task-definition.json"
}
```

Finally, we can create our service. We'll create a file called `ecs-create-service.json` in our project directory. In `ecs-create-service.json`, we'll specify the name of our service, the task definition that our service will use, the number of tasks that our service will run, and the load balancer that our service will use. 

```json
{
  "service": "my-microservice-service",
  "taskDefinition": "my-microservice-task-definition",
  "desiredCount": 1,
  "loadBalancer": {
    "elbName": "my-load-balancer",
    "targetGroupArn": "arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-target-group/abcdef1234567890"
  }
}
```

Now that we have our `ecs-create-service.json` file, we can deploy our service. We'll use the [AWS Command Line Interface (CLI)](https://aws.amazon.com/cli/) to deploy our service. First, we'll use the `aws ecs register-task-definition` command to register our task definition. 

```bash
aws ecs register-task-definition --cli-input-json file://ecs-register-task-definition.json
```

Next, we'll use the `aws ecs create-service` command to create our service. 

```bash
aws ecs create-service --cli-input-json file://ecs-create-service.json
```

## Conclusion

In this article, we've explored how to develop a microservice using TypeScript and Nest.js. We've looked at the benefits of using TypeScript and Nest.js for microservices. We've also created a simple microservice and deployed it to a server.