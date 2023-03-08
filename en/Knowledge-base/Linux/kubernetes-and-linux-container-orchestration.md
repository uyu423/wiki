---
title: Kubernetes and Linux Container Orchestration
description: 
published: true
date: 2023-02-12T03:32:16.366Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:32:14.471Z
---

- [Orquestación de contenedores de Kubernetes y Linux***Spanish** document is available*](/es/Knowledge-base/Linux/kubernetes-and-linux-container-orchestration)
{.links-list}
- [Kubernetes 和 Linux 容器编排***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/kubernetes-and-linux-container-orchestration)
{.links-list}
- [Kubernetes 및 Linux 컨테이너 오케스트레이션***Korean** document is available*](/ko/Knowledge-base/Linux/kubernetes-and-linux-container-orchestration)
{.links-list}


# What is Kubernetes?

Kubernetes is an open source container orchestration platform originally designed by Google. It is now maintained by the Cloud Native Computing Foundation. It can be used to automate the deployment, scaling, and management of containerized applications.

# What is a Linux Container?

A Linux container is a software package that contains all the necessary components to run an application or service in a isolated environment. Containers are an alternative to Virtual Machines and can provide many benefits such as improved resource utilization, portability, and security.

# Kubernetes and Linux Container Orchestration

Kubernetes is often used for container orchestration, which is the management of multiple containers. This can include tasks such as deploying, scaling, and monitoring containers. Linux containers can be used with Kubernetes to provide a lightweight and portable application environment.

# Getting Started with Kubernetes

There are a few Kubernetes installation options, including using a hosted solution or installing it on your own infrastructure. For development and testing purposes, you can also use a single-node Kubernetes cluster, which can be run on a Linux container platform such as Docker.

Once you have Kubernetes installed, you can start deploying applications. To do this, you will need to create a Kubernetes deployment file. This file contains all the necessary information about your application, such as the container image to use, the number of replicas, and any exposed ports.

Here is an example deployment file for a simple PHP application:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-php-app
  labels:
    app: my-php-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-php-app
  template:
    metadata:
      labels:
        app: my-php-app
    spec:
      containers:
      - name: my-php-app
        image: php:7.2-apache
        ports:
        - containerPort: 80
```

This file can be used to deploy the application by running the following command:

```
$ kubectl apply -f my-php-app.yaml
```

# Conclusion

Kubernetes is a powerful tool for managing containerized applications. It can be used to automate the deployment, scaling, and management of containers. Linux containers can be used with Kubernetes to provide a lightweight and portable application environment.