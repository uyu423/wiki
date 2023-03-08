---
title: 035: Building and deploying a Spring Boot application to container orchestration platforms (Kubernetes, Docker Swarm)
description: 
published: true
date: 2023-02-04T03:32:39.892Z
tags: 
editor: markdown
dateCreated: 2023-02-04T03:32:38.115Z
---

- [035: Creación e implementación de una aplicación Spring Boot en plataformas de orquestación de contenedores (Kubernetes, Docker Swarm)***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/035-building-and-deploying-a-spring-boot-application-to-container-orchestration-platforms-kubernetes-docker-swarm)
{.links-list}
- [035：构建 Spring Boot 应用程序并将其部署到容器编排平台（Kubernetes、Docker Swarm）***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/035-building-and-deploying-a-spring-boot-application-to-container-orchestration-platforms-kubernetes-docker-swarm)
{.links-list}
- [035: 컨테이너 오케스트레이션 플랫폼(Kubernetes, Docker Swarm)에 Spring Boot 애플리케이션 빌드 및 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/035-building-and-deploying-a-spring-boot-application-to-container-orchestration-platforms-kubernetes-docker-swarm)
{.links-list}


# 035: Building and deploying a Spring Boot application to container orchestration platforms (Kubernetes, Docker Swarm)

Spring Boot is a popular Java-based framework used for developing microservices. In this post, we'll learn how to containerize a Spring Boot application and deploy it to Kubernetes and Docker Swarm.

## Containerizing a Spring Boot application

To containerize a Spring Boot application, we'll first need to create a `Dockerfile`. A `Dockerfile` is a text file that contains instructions for building a Docker image.

We'll start by creating a `Dockerfile` in the root directory of our Spring Boot project.

```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

In this `Dockerfile`, we're using `openjdk:8-jdk-alpine` as our base image. We're also using a `VOLUME` to create a mount point for storing temporary files.

Next, we'll copy our Spring Boot `.jar` file into the container as `app.jar` and set it as the `ENTRYPOINT`.

Now that we have our `Dockerfile`, we can build our Docker image. We'll use the `docker build` command to build our image, tagging it with the `latest` tag.

```
$ docker build -t my-spring-boot-app:latest .
```

## Deploying to Kubernetes

Kubernetes is a popular container orchestration platform. It can be used to manage a group of containers as a single unit.

To deploy our Spring Boot application to Kubernetes, we'll first need to create a `Deployment`. A `Deployment` defines a group of identical pods and ensures that a certain number of them are always running.

We'll create a `deployment.yaml` file in the root directory of our project.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-spring-boot-app
  labels:
    app: my-spring-boot-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-spring-boot-app
  template:
    metadata:
      labels:
        app: my-spring-boot-app
    spec:
      containers:
      - name: my-spring-boot-app
        image: my-spring-boot-app:latest
        ports:
        - containerPort: 8080
```

In this file, we've defined a `Deployment` with a replica count of 3. We've also defined a `selector` and `template` which specify the pods that the `Deployment` will manage.

Now, we can create our `Deployment` in Kubernetes using the `kubectl` command-line tool.

```
$ kubectl apply -f deployment.yaml
```

## Deploying to Docker Swarm

Docker Swarm is a container orchestration platform from Docker. It can be used to manage a group of Docker containers as a single unit.

To deploy our Spring Boot application to Docker Swarm, we'll first need to create a `Stack`. A `Stack` is a group of services that are deployed together.

We'll create a `stack.yaml` file in the root directory of our project.

```yaml
version: "3.1"

services:

  my-spring-boot-app:
    image: my-spring-boot-app:latest
    ports:
      - "8080:8080"
    deploy:
      replicas: 3
```

In this file, we've defined a `Stack` with a single service, `my-spring-boot-app`. We've also specified that we want 3 replicas of this service to be deployed.

Now, we can deploy our `Stack` to Docker Swarm using the `docker stack` command.

```
$ docker stack deploy -c stack.yaml my-spring-boot-app
```

## Additional Information

- If you're using Kubernetes, you can also create a `Service` to expose your application to the outside world.
- If you're using Docker Swarm, you can also create a `Network` to allow communication between your services.

## Resources for further reading

- [Spring Boot Reference Documentation - Containerizing Spring Boot Applications](https://docs.spring.io/spring-boot/docs/current/reference/html/deploying-spring-boot.html#deploying-spring-boot-containerizing)
- [Kubernetes Documentation - Creating a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment)
- [Docker Documentation - Deploy a Stack to a Swarm](https://docs.docker.com/engine/reference/commandline/stack_deploy/#deploy-a-stack-to-a-swarm)