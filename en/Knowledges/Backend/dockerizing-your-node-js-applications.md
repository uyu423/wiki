---
title: Dockerizing your Node.js applications
description: 
published: true
date: 2023-01-29T16:40:25.450Z
tags: 
editor: markdown
dateCreated: 2023-01-29T16:40:25.450Z
---


# Dockerizing your Node.js Applications
Docker is a popular containers platform that continues to grow in popularity since its inception in 2013. It allows developers to package their applications into small, lightweight containers for easy deployment on any platform. By leveraging the lightweight nature of Docker containers, developers can quickly and easily deploy Node.js applications across multiple machines, ensuring maximum performance and reliability.

In this guide, we'll take a look at the basics of Dockerizing your Node.js applications. We will cover setting up your environment, creating a Docker image, and deploying your application to the cloud. By the end of this guide, you'll have a fully running Node.js application hosted in the cloud using Docker.

## Prerequisites 
Before you get started, you'll need to make sure you have the following installed on your machine:

* Docker
* Node.js
* NPM

If you don't already have Docker installed, you can follow the installation instructions for your operating system from the official site. Once Docker is installed, you can move on to installing Node.js and NPM. 

## Writing the Node.js Application 
For the sake of this guide, we'll be using a simple Node.js application written with the Express framework. This application will simply display a “Hello World” message when a request is made to the root path of the server.

Begin by creating a new directory for your application:

```
$ mkdir my-node-app
$ cd my-node-app
```

Next, initialize the project with NPM:

```
$ npm init
```

Follow the prompts to create a package.json file for your application, which will be used later on when creating the Docker image. 

Next, we can install the Express framework and related packages:

```
$ npm install express
$ npm install body-parser
```

Finally, write the application code and save it to a new file named `index.js`:

```
const express = require('express')
const bodyParser = require('body-parser')
const app = express()

app.use(bodyParser.urlencoded({ extended: true }))
app.use(bodyParser.json())

app.get('/', (req, res) => {
  res.send('Hello World!')
})

// Start server
const port = process.env.PORT || 3000
app.listen(port)
```

At this point, you should have a basic Node.js application written and ready to be Dockerized. 

## Creating the Docker Image
Now that we have the application written, we can move on to creating the Docker image. A Docker image is a reusable snapshot of our application. Whenever the image is run, it will start a container with our application code running inside of it. 

To create the Docker image, we'll need to create a Dockerfile. A Dockerfile is a text file that contains the commands to build the image. Begin by creating a new file in your project directory named `Dockerfile`.

Add the following to the file:

```
FROM node:8

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json .

RUN npm install

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "node", "index.js" ]
```

This Dockerfile will start from the official Node.js 8 image, create a working directory for the application, install any dependencies from the `package.json` file, copy the application code into the image, expose port 3000, and then run the application on start. 

Now that we have the Dockerfile created, we can build the image. To build the image, use the `docker build` command:

```
$ docker build -t my-node-app .
```

This command will take a few minutes while it downloads the necessary Node.js image, installs any dependencies, and creates the image. Once the image is built, we can move on to deploying it.

## Deploying the Docker Image 
Now that we have our Docker image created, we can deploy it to the cloud. We'll be using a service called Docker Hub to deploy the image. Docker Hub is a hosting service for Docker images. It provides an easy way to share and distribute images with others.

To begin, create an account on Docker Hub if you don't already have one. After you have your account created, log into the Docker Hub web portal, and select the “Create” option.

On the next screen, select “Create Repository” and give your repository a name. For this tutorial we'll use the name “my-node-app”. Once the repository is created, you will be given a URL to push the image to. 

Next, we can use the `docker push` command to push the image to Docker Hub. The command will look something like this:

```
$ docker push {username}/my-node-app
```

where `{username}` is your Docker Hub username. When the command is run, the image will be uploaded to Docker Hub and available for anyone to download and use. 

## Running the Application 
Now that we've pushed our image to Docker Hub, we can start a container and run the application. We'll be using the `docker run` command, which works similarly to the `docker push` command. The command will look something like this:

```
$ docker run -d -p 80:3000 {username}/my-node-app
```

This command will run the application in a detached mode, mapping port 80 of the host machine to port 3000 of the container. This will allow us to access the application by simply visiting `localhost` in a browser. 

Once the container is running, you should see the “Hello World” message being displayed in the browser. Congratulations, you've just deployed a Node.js application using Docker!

## Summary 
In this guide, we showed you how to Dockerize your Node.js applications. We started by setting up your environment, then writing a Node.js application using the Express framework. We then created a Docker image for the application, pushed it to Docker Hub, and then ran it in a container. By the end of this guide, you should have a fully running Node.js application in the cloud.

In summary, we covered the following topics:

- Setting up your environment
- Writing a Node.js application
- Creating a Docker image
- Deploying the Docker image to Docker Hub
- Running the application

We hope this guide has been helpful in getting you started Dockerizing your Node.js applications. 

- Installing Docker, Node.js and NPM 
- Writing the Node.js application 
- Creating the Docker image 
- Deploying the Docker image
- Running the application 
- Summary