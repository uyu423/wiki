---
title: Building Scalable Applications with Kubernetes and Docker
description: 
published: true
date: 2023-01-29T23:56:10.898Z
tags: 
editor: markdown
dateCreated: 2023-01-29T23:56:10.898Z
---

- [Kubernetes 및 Docker로 확장 가능한 애플리케이션 구축***Korean** version of this document is available*](/ko/Knowledge-base/Backend/building-scalable-applications-with-kubernetes-and-docker)
{.links-list}


Docker and Kubernetes are two of the most popular tools for developing and deploying software applications. They are both powerful tools that can help you develop and deploy scalable applications.

Docker is a tool that makes it easy to package and deploy your applications. Kubernetes is a tool that helps you manage and scale your applications.

In this article, we will discuss how to use Docker and Kubernetes to develop and deploy scalable applications.

Docker is a tool that makes it easy to package and deploy your applications. It is a great tool for developing and deploying microservices. Microservices are small, independent, and can be deployed and scaled independently.

Docker allows you to package your application into a container. A container is a self-contained image that contains all the dependencies and libraries that your application needs to run.

You can then deploy your containerized application to any environment that supports Docker. This makes it easy to deploy your application to development, staging, and production environments.

Kubernetes is a tool that helps you manage and scale your applications. It is designed for running distributed systems.

Kubernetes allows you to deploy and manage your applications at scale. It also provides features such as self-healing, horizontal scaling, and load balancing.

Kubernetes is a great choice for deploying and managing stateful applications. Stateful applications are applications that maintain data state. Examples of stateful applications are databases, key-value stores, and message queues.

Kubernetes is also a good choice for deploying and managing stateless applications. Stateless applications are applications that do not maintain any data state. Examples of stateless applications are web applications and microservices.

In this article, we will discuss how to use Docker and Kubernetes to develop and deploy a stateless web application.

We will use the following tools:

Docker

Kubernetes

Git

 Jenkins

Our application will be a simple Node.js application that prints "Hello, World!"

We will use Jenkins to build and deploy our application.

First, we will create a new Jenkins job. We will name our job "chatgpt-nodejs-app".

Next, we will configure our job to use the "Git" source code management system. We will use the following Git repository:

https://github.com/chatgpt/chatgpt-nodejs-app

We will also configure our job to use the "Docker" Build step. We will use the following Dockerfile:

FROM node:12.2.0-alpine RUN mkdir -p /usr/src/app WORKDIR /usr/src/app COPY . . RUN npm install EXPOSE 3000 CMD [ "npm", "start" ]

This Dockerfile will create a Docker image that contains our Node.js application.

Next, we will configure our job to use the "Kubernetes" Deploy step. We will use the following Kubernetes manifest:

apiVersion: apps/v1 kind: Deployment metadata: name: chatgpt-nodejs-app namespace: default spec: replicas: 1 selector: matchLabels: app: chatgpt-nodejs-app template: metadata: labels: app: chatgpt-nodejs-app spec: containers: - name: chatgpt-nodejs-app image: chatgpt/chatgpt-nodejs-app:latest ports: - containerPort: 3000

This Kubernetes manifest will deploy our application to a Kubernetes cluster.

Lastly, we will configure our job to use the "Publish Over SSH" post-build action. We will use the following server configuration:

- name: chatgpt-k8s-master hostname: chatgpt-k8s-master.default.svc.cluster.local user: root port: 22 command: kubectl rollout restart deployment chatgpt-nodejs-app

This post-build action will restart our Kubernetes deployment.

Now, we will create a Jenkins pipeline. A pipeline is a series of steps that our Jenkins job will execute.

We will name our pipeline "chatgpt-nodejs-app-pipeline".

Next, we will configure our pipeline to use the "Git" source code management system. We will use the following Git repository:

https://github.com/chatgpt/chatgpt-nodejs-app

We will also configure our pipeline to use the "Docker" Build step. We will use the following Dockerfile:

FROM node:12.2.0-alpine RUN mkdir -p /usr/src/app WORKDIR /usr/src/app COPY . . RUN npm install EXPOSE 3000 CMD [ "npm", "start" ]

This Dockerfile will create a Docker image that contains our Node.js application.

Next, we will configure our pipeline to use the "Kubernetes" Deploy step. We will use the following Kubernetes manifest:

apiVersion: apps/v1 kind: Deployment metadata: name: chatgpt-nodejs-app namespace: default spec: replicas: 1 selector: matchLabels: app: chatgpt-nodejs-app template: metadata: labels: app: chatgpt-nodejs-app spec: containers: - name: chatgpt-nodejs-app image: chatgpt/chatgpt-nodejs-app:latest ports: - containerPort: 3000

This Kubernetes manifest will deploy our application to a Kubernetes cluster.

Lastly, we will configure our pipeline to use the "Publish Over SSH" post-build action. We will use the following server configuration:

- name: chatgpt-k8s-master hostname: chatgpt-k8s-master.default.svc.cluster.local user: root port: 22 command: kubectl rollout restart deployment chatgpt-nodejs-app

This post-build action will restart our Kubernetes deployment.

Now, we will trigger our pipeline. We will do this by committing our code to the Git repository.

Our pipeline will build our Docker image, deploy our Kubernetes manifest, and restart our Kubernetes deployment.

Once our pipeline has completed, we will have a running Node.js application that prints "Hello, World!"

You can find the source code for this article on GitHub.