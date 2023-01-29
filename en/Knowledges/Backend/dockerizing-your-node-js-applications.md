---
title: Dockerizing your Node.js applications
description: 
published: true
date: 2023-01-29T16:22:21.606Z
tags: 
editor: markdown
dateCreated: 2023-01-29T16:22:21.606Z
---



{.markdown}

Docker is a great tool for automating the deployment of your applications. It allows you to package your application into a self-contained image that can be deployed on any Docker host.

Dockerizing your Node.js applications is a great way to increase the development speed and reduce the friction when working with collaborators. In this article, we will show you how to dockerize a Node.js application and run it on a Docker host.

We will be using the popular Express framework to build our Node.js application. Express is a fast, unopinionated, minimalist web framework for Node.js.

The first thing we need to do is to create a package.json file that contains the dependencies for our Node.js application. We can do this by running the following command:

```
npm init
```

Once the package.json file is created, we can install the Express framework by running the following command:

```
npm install --save express
```

Now that we have the Express framework installed, we can create a simple Node.js application that will print "Hello World" when we access it in a web browser.

Create a file named app.js and add the following code to it:

```javascript
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World');
});

app.listen(3000, function () {
  console.log('Example app listening on port 3000');
});
```

This code creates a simple Express application that will listen on port 3000 and print "Hello World" when we access the root URL.

Now that we have our Node.js application ready, we can dockerize it.

The first thing we need to do is to create a Dockerfile. A Dockerfile is a text file that contains the instructions for building a Docker image.

Create a file named Dockerfile and add the following contents to it:

```
FROM node:8
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

This Dockerfile uses the node:8 Docker image as the base image. It then creates a working directory named /app and copies the package.json file into it. It then runs the npm install command to install the dependencies for our Node.js application. Finally, it copies the app.js file into the /app directory and exposes port 3000.

Now that we have our Dockerfile ready, we can build a Docker image from it.

run the following command to build a Docker image named my-node-app from the Dockerfile:

```
docker build -t my-node-app .
```

This command will build a Docker image named my-node-app from the current directory.

Now that we have our Docker image built, we can run it as a Docker container.

Run the following command to start a Docker container from the my-node-app image:

```
docker run -d -p 3000:3000 my-node-app
```

This command will start a Docker container from the my-node-app image and expose port 3000.

You can now access your Node.js application in a web browser by going to http://localhost:3000.

Docker is a great tool for automating the deployment of your Node.js applications. It allows you to package your application into a self-contained image that can be deployed on any Docker host.

Dockerizing your Node.js applications is a great way to increase the development speed and reduce the friction when working with collaborators. In this article, we showed you how to dockerize a Node.js application and run it on a Docker host.