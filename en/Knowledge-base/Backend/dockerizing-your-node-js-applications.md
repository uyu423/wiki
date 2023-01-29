---
title: Dockerizing your Node.js applications
description: 
published: true
date: 2023-01-29T17:19:47.114Z
tags: 
editor: markdown
dateCreated: 2023-01-29T17:19:47.114Z
---


#Dockerizing your Node.js applications

Docker is a tool that enables you to package and run your applications in isolated environments called containers. By packaging your Node.js applications into containers, you can ship them anywhere and run them easily and consistently on any platform.

There are many benefits to using containers for Node.js applications. Containers are lightweight and portable, and they offer a consistent environment for your application to run in. This is especially important for Node.js applications, which are often run on multiple servers and can be difficult to keep consistent.

In this post, we'll show you how to package your Node.js applications into Docker containers. We'll also show you how to use Docker Compose to manage your containers.

##Dockerizing a Node.js application

To dockerize a Node.js application, you need a `Dockerfile`. This file contains all the instructions that Docker needs to build your image.

Here's a simple `Dockerfile` for a Node.js application:

```
#Dockerfile

FROM node:alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

Let's break down this `Dockerfile`:

- `FROM node:alpine`: This instruction tells Docker to use the `node` image as the base for our image. We're using the `alpine` version of the node image, which is a smaller, lighter version of the node image.

- `WORKDIR /app`: This instruction sets the working directory for the rest of the instructions in the `Dockerfile`. All the subsequent instructions will be run in this directory.

- `COPY package*.json ./`: This instruction copies the `package.json` and `package-lock.json` files from the current directory into the `/app` directory.

- `RUN npm install`: This instruction runs the `npm install` command to install the dependencies for our application.

- `COPY . .`: This instruction copies the rest of the files from the current directory into the `/app` directory.

- `EXPOSE 3000`: This instruction tells Docker that our application is listening on port 3000.

- `CMD ["npm", "start"]`: This instruction tells Docker to run the `npm start` command when the container is started. This will start our application.

Now that we have a `Dockerfile`, we can build our image. To do this, we run the `docker build` command:

```
$ docker build -t my-app .
```

This will build an image with the tag `my-app`. You can see your image by running the `docker images` command:

```
$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
my-app              latest              fce289e99eb9        1 minute ago        67.1MB
node                alpine              4d0eb22ecb8e        6 weeks ago         67.1MB
```

Now that we have our image, we can run it. To do this, we use the `docker run` command:

```
$ docker run -d -p 3000:3000 my-app
```

This will start a container from our `my-app` image and expose port 3000 on the host machine. The `-d` flag tells Docker to run the container in detached mode, which means the container will run in the background.

You can see your running container by running the `docker ps` command:

```
$ docker ps

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                  NAMES
b73a96b50a2f        my-app              "npm start"         5 seconds ago       Up 4 seconds        0.0.0.0:3000->3000/tcp   my-app
```

You can also view the logs for your container by running the `docker logs` command:

```
$ docker logs my-app

> my-app@1.0.0 start /app
> node index.js

Listening on port 3000
```

##Docker Compose

Docker Compose is a tool for managing multiple containers. With Compose, you can define all your application's containers in a single `docker-compose.yml` file.

Here's an example `docker-compose.yml` file:

```
version: '3'

services:
  web:
    build: .
    ports:
     - "3000:3000"
    volumes:
     - .:/app
    depends_on:
     - db

  db:
    image: mongo
    ports:
     - "27017:27017"
    volumes:
     - ./data:/data/db
```

This `docker-compose.yml` file defines two services: `web` and `db`. The `web` service is our Node.js application, and the `db` service is a MongoDB database.

The `web` service is built from the `Dockerfile` in the current directory. It's exposed on port 3000 and is linked to the `db` service. The `volumes` instruction mounts the current directory into the container so that changes to the code are automatically picked up.

The `db` service is built from the `mongo` image. It's exposed on port 27017 and is linked to the `web` service. The `volumes` instruction mounts the `./data` directory into the container so that the data is persisted outside the container.

With Compose, we can start all our services with a single command:

```
$ docker-compose up
```

This will start all our services in the background. We can see the logs for our services with the `docker-compose logs` command:

```
$ docker-compose logs

Attaching to my-app_web_1, my-app_db_1
web_1   | > my-app@1.0.0 start /app
web_1   | > node index.js
web_1   |
web_1   | Listening on port 3000
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] MongoDB starting : pid=1 port=27017 dbpath=/data/db 64-bit host=b73a96b50a2f
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] db version v3.6.3
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] git version: a69dfe61e2e1fc0bcad6c2f6f26a1a0e3f6c5a18
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.2o  27 Mar 2018
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] allocator: tcmalloc
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] modules: none
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] build environment:
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten]     distmod: ubuntu1604
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten]     distarch: x86_64
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten]     target_arch: x86_64
db_1    | 2018-12-10T18:46:43.790+0000 I CONTROL  [initandlisten] options: {}
db_1    | 2018-12-10T18:46:43.815+0000 I STORAGE  [initandlisten] wiredtiger_open config: create,cache_size=36M,session_max=20000,eviction=(threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,archive=true,path=journal,compressor=snappy),file_manager=(close_idle_time=100000),statistics_log=(wait=0),
db_1    | 2018-12-10T18:46:43.943+0000 I CONTROL  [initandlisten] ** WARNING: Access control