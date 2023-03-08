---
title: 078: Deploying TensorFlow.js Applications on Raspberry Pi with Node.js
description: 
published: true
date: 2023-02-03T01:04:43.585Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:04:38.871Z
---

- [078: Implementación de aplicaciones TensorFlow.js en Raspberry Pi con Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/078-deploying-tensorflow-js-applications-on-raspberry-pi-with-node-js)
{.links-list}
- [078：使用 Node.js 在 Raspberry Pi 上部署 TensorFlow.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/078-deploying-tensorflow-js-applications-on-raspberry-pi-with-node-js)
{.links-list}
- [078: Node.js를 사용하여 Raspberry Pi에 TensorFlow.js 애플리케이션 배포***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/078-deploying-tensorflow-js-applications-on-raspberry-pi-with-node-js)
{.links-list}


## Introduction

Raspberry Pi is a credit card sized computer that can be used for various electronics projects. It has a wide range of applications and can be used in various fields such as education, industry, and research.

One of the most popular applications of Raspberry Pi is to use it as an edge device for machine learning. TensorFlow.js is a JavaScript library for training and deploying machine learning models.

In this post, we will guide you through the process of setting up a Raspberry Pi for TensorFlow.js. We will also show you how to deploy a TensorFlow.js application on the Raspberry Pi.

## Setting up Raspberry Pi

The first thing you need to do is to set up your Raspberry Pi. You can follow the instructions in this link: https://www.raspberrypi.org/documentation/setup/

Once your Raspberry Pi is set up, you need to install Node.js on it. Node.js is a JavaScript runtime that is required for running TensorFlow.js applications.

You can install Node.js on Raspberry Pi by following the instructions in this link: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager

## Deploying TensorFlow.js Applications

Once you have Node.js installed, you can now deploy TensorFlow.js applications on your Raspberry Pi.

There are two ways to deploy TensorFlow.js applications:

1. Use a web server to serve the application.
2. Use a command line tool to deploy the application.

### Using a Web Server

The first method is to use a web server to serve the application. We will use the Node.js web server, Express.js.

Express.js is a web application framework for Node.js. It is used for building web applications and APIs.

You can install Express.js by running the following command:

```
npm install express --save
```

Once Express.js is installed, you can create a file named `app.js` and add the following code to it:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello world!');
});

app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

This code creates a web server that responds to HTTP requests with the string `Hello world!`.

You can start the web server by running the following command:

```
node app.js
```

You can now access the web server at http://localhost:3000.

### Using a Command Line Tool

The second method is to use a command line tool to deploy the application. We will use the TensorFlow.js CLI.

The TensorFlow.js CLI is a command line tool that can be used for training, deploying, and working with TensorFlow.js models.

You can install the TensorFlow.js CLI by running the following command:

```
npm install -g @tensorflow/tfjs-node
```

Once the TensorFlow.js CLI is installed, you can use it to deploy a TensorFlow.js application.

Let's say you have a TensorFlow.js application in the `app` directory. You can deploy the application by running the following command:

```
tfjs deploy --dir app
```

This will start a web server that serves the TensorFlow.js application. You can access the application at http://localhost:3000.

## Conclusion

In this post, we have shown you how to deploy TensorFlow.js applications on Raspberry Pi. We have also shown you how to use a web server to serve the application.