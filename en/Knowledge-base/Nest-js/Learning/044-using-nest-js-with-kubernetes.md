---
title: 044: Using Nest.js with Kubernetes
description: 
published: true
date: 2023-02-15T16:33:20.812Z
tags: 
editor: markdown
dateCreated: 2023-02-15T16:33:13.079Z
---

- [044: Uso de Nest.js con Kubernetes***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/044-using-nest-js-with-kubernetes)
{.links-list}
- [044：将 Nest.js 与 Kubernetes 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/044-using-nest-js-with-kubernetes)
{.links-list}
- [044: 쿠버네티스와 함께 Nest.js 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/044-using-nest-js-with-kubernetes)
{.links-list}


# Using Nest.js with Kubernetes

Kubernetes is a powerful container orchestration tool, and Nest.js is a popular Node.js framework. In this post, we'll show you how to use Nest.js with Kubernetes.

## Prerequisites

- A Kubernetes cluster
- A text editor

## Installing Nest.js

First, we need to install Nest.js. We can do this using the Node.js package manager, npm:

```
npm install -g @nestjs/cli
```

## Creating a Nest.js Project

Once Nest.js is installed, we can create a new project using the Nest.js CLI:

```
nest new project-name
```

## Running a Nest.js Project

We can run our Nest.js project using the following command:

```
npm run start
```

## Deploying a Nest.js Project to Kubernetes

We can deploy our Nest.js project to Kubernetes using the kubectl command line tool.

First, we need to create a file called `nest-deployment.yaml` with the following contents:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nest-deployment
spec:
  selector:
    matchLabels:
      app: nest
  replicas: 2
  template:
    metadata:
      labels:
        app: nest
    spec:
      containers:
      - name: nest
        image: YOUR_DOCKER_HUB_USERNAME/nest
        ports:
        - containerPort: 8080
```

Replace `YOUR_DOCKER_HUB_USERNAME` with your Docker Hub username.

Next, we need to build our Nest.js project and push it to Docker Hub:

```
docker build -t YOUR_DOCKER_HUB_USERNAME/nest .
docker push YOUR_DOCKER_HUB_USERNAME/nest
```

Finally, we can deploy our Nest.js project to Kubernetes:

```
kubectl apply -f nest-deployment.yaml
```

## Accessing a Nest.js Application

We can access our Nest.js application via the Kubernetes cluster IP address:

```
http://CLUSTER_IP:8080
```

Replace `CLUSTER_IP` with the IP address of your Kubernetes cluster.

## Conclusion

In this post, we've shown you how to use Nest.js with Kubernetes. We've installed Nest.js, created a new project, and deployed it to Kubernetes. We've also shown you how to access your Nest.js application via the Kubernetes cluster IP address.