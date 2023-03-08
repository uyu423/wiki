---
title: 086: Deploying a Spring Boot Application to Kubernetes
description: 
published: true
date: 2023-02-05T16:32:21.528Z
tags: 
editor: markdown
dateCreated: 2023-02-05T16:32:16.113Z
---

- [086: Implementación de una aplicación Spring Boot en Kubernetes***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/086-deploying-a-spring-boot-application-to-kubernetes)
{.links-list}
- [086：将 Spring Boot 应用程序部署到 Kubernetes***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/086-deploying-a-spring-boot-application-to-kubernetes)
{.links-list}
- [086: Kubernetes에 Spring Boot 애플리케이션 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/086-deploying-a-spring-boot-application-to-kubernetes)
{.links-list}


# 086: Deploying a Spring Boot Application to Kubernetes

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

Spring Boot is a popular Java framework for building web applications and microservices.

In this post, we'll show you how to deploy a Spring Boot application to Kubernetes.

## Prerequisites

- A Kubernetes cluster
- A Spring Boot application

## Deploying the Application

1. Create a Kubernetes deployment for your application.

   ```
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: myapp-deployment
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: myapp
     template:
       metadata:
         labels:
           app: myapp
       spec:
         containers:
         - name: myapp-container
           image: myapp-image
           ports:
           - containerPort: 8080
   ```

2. Create a Kubernetes service for your application.

   ```
   apiVersion: v1
   kind: Service
   metadata:
     name: myapp-service
   spec:
     type: LoadBalancer
     ports:
     - port: 80
       targetPort: 8080
     selector:
       app: myapp
   ```

3. Apply the deployment and service to your Kubernetes cluster.

   ```
   kubectl apply -f myapp-deployment.yaml
   kubectl apply -f myapp-service.yaml
   ```

4. Check that the deployment and service are running.

   ```
   kubectl get deployment
   kubectl get service
   ```

Your application is now deployed to Kubernetes!

## Additional Information

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)