---
title: Dockerizing your Node.js applications
description: 
published: true
date: 2023-01-29T16:20:24.761Z
tags: 
editor: markdown
dateCreated: 2023-01-29T16:20:24.761Z
---


- [Dockerizing your node.js applications]('https://blog.logrocket.com/dockerizing-your-node-js-applications-a49oaebufyay')
- [Dockerize a Node.js web app]('https://nodejs.org/en/docs/guides/nodejs-docker-webapp/')
- [How to Dockerize a Node.js App]('https://medium.com/@goldensunliu/how-to-dockerize-a-node-js-app-eb2126e392bb')



Docker is a great platform for packaging and running Node.js applications. It’s easy to set up, it’s lightweight, and it has a huge ecosystem of tools and plugins.

Dockerizing a Node.js application is a pretty simple process. In this post, we’ll go over the basics of setting up a Node.js application and dockerizing it so that it can be run in a container.

We’ll start by creating a simple Node.js web server. Then, we’ll install the necessary dependencies and set up a Dockerfile so that our application can be built into a Docker image. Finally, we’ll run our application in a Docker container.

Creating a Node.js web server

The first thing we need to do is create a file called server.js in our project’s root directory. This file will contain the code for our simple Node.js web server.

We’ll start by requiring the http module, which is a built-in module in Node.js. This module will give us the ability to create a web server.

Next, we’ll create a server object using the http.createServer() method. This method takes a callback function as an argument. This callback function will be invoked when the server receives a request.

Inside the callback function, we’ll use the response object’s writeHead() method to send a response header with a status code of 200 and a content-type of text/plain .

Then, we’ll use the response object’s end() method to send the response body. In this case, we’ll just send a simple string: Hello, World! .

Finally, we’ll use the server’s listen() method to start listening for requests on a specified port. In this case, we’ll specify port 3000.

Here’s the code for our server.js file:

```
const http = require('http');

const server = http.createServer((request, response) => {
  response.writeHead(200, { 'Content-Type': 'text/plain' });
  response.end('Hello, World!');
});

server.listen(3000);
```

Now that we have our Node.js web server set up, we can test it by running the following command in our terminal:

```
node server.js
```

If everything is working as expected, you should see the following output in your terminal:

```
$ node server.js
```

Now, we can open a web browser and navigate to http://localhost:3000 . We should see our “Hello, World!” message.

Installing dependencies and creating a Dockerfile

Now that we have a basic Node.js web server up and running, we can install the necessary dependencies and set up a Dockerfile so that our application can be built into a Docker image.

First, we’ll install the Express.js web framework. Express.js is a popular web framework for Node.js. It’s lightweight and easy to use, and it’s perfect for getting a web server up and running quickly.

We can install Express.js by running the following command in our terminal:

```
npm install express
```

After the installation is complete, we should see a new directory called node_modules in our project’s root directory. This directory contains all of the dependencies for our project.

Next, we’ll create a file called Dockerfile in our project’s root directory. This file will contain the instructions for building our Docker image.

We’ll start by specifying the base image that our image will be built on top of. In this case, we’ll use the node:8.9.4-alpine image, which is a minimal Docker image for Node.js.

Next, we’ll specify the working directory for our image. This is the directory that our application’s files will be copied to. In this case, we’ll use the /app directory.

Then, we’ll copy the package.json and package-lock.json files from our project’s root directory into the /app directory. These files contain the dependencies for our project.

After that, we’ll use the npm install command to install our project’s dependencies.

Finally, we’ll copy the server.js file from our project’s root directory into the /app directory. This is the file that contains the code for our Node.js web server.

Here’s the code for our Dockerfile:

```
FROM node:8.9.4-alpine

WORKDIR /app

COPY package.json .
COPY package-lock.json .

RUN npm install

COPY server.js .

ENTRYPOINT ["node", "server.js"]
```

Now that we have our Dockerfile set up, we can build our Docker image by running the following command in our terminal:

```
docker build -t node-docker .
```

This command will build a Docker image called node-docker using the instructions in our Dockerfile.

Running our application in a Docker container

Now that we have our Docker image, we can run our application in a Docker container.

We can do this by running the following command in our terminal:

```
docker run -p 3000:3000 node-docker
```

This command will start a Docker container from our node-docker image and map port 3000 on the host machine to port 3000 in the container.

Now, we can open a web browser and navigate to http://localhost:3000 . We should see our “Hello, World!” message.

Conclusion

In this post, we’ve gone over the basics of setting up a Node.js application and dockerizing it so that it can be run in a container.

If you’re interested in learning more about Docker, be sure to check out the official Docker documentation.