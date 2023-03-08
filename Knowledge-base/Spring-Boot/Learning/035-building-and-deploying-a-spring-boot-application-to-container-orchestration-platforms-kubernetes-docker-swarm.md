---
title: 035: 컨테이너 오케스트레이션 플랫폼(Kubernetes, Docker Swarm)에 Spring Boot 애플리케이션 빌드 및 배포
description: 
published: true
date: 2023-02-04T03:32:43.466Z
tags: 
editor: markdown
dateCreated: 2023-02-04T03:32:38.111Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [035: Building and deploying a Spring Boot application to container orchestration platforms (Kubernetes, Docker Swarm)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/035-building-and-deploying-a-spring-boot-application-to-container-orchestration-platforms-kubernetes-docker-swarm)
{.links-list}


# 035: 컨테이너 오케스트레이션 플랫폼(Kubernetes, Docker Swarm)에 Spring Boot 애플리케이션 빌드 및 배포

Spring Boot는 마이크로서비스 개발에 사용되는 널리 사용되는 Java 기반 프레임워크입니다. 이 게시물에서는 Spring Boot 애플리케이션을 컨테이너화하고 이를 Kubernetes 및 Docker Swarm에 배포하는 방법을 알아봅니다.

## Spring Boot 애플리케이션 컨테이너화

Spring Boot 애플리케이션을 컨테이너화하려면 먼저 `Dockerfile`을 생성해야 합니다. `Dockerfile`은 Docker 이미지를 빌드하기 위한 지침이 포함된 텍스트 파일입니다.

Spring Boot 프로젝트의 루트 디렉토리에 `Dockerfile`을 생성하여 시작하겠습니다.

```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

이 `Dockerfile`에서는 `openjdk:8-jdk-alpine`을 기본 이미지로 사용하고 있습니다. 또한 `VOLUME`을 사용하여 임시 파일을 저장하기 위한 마운트 지점을 생성합니다.

다음으로 Spring Boot `.jar` 파일을 컨테이너에 `app.jar`로 복사하고 `ENTRYPOINT`로 설정합니다.

이제 `Dockerfile`이 있으므로 Docker 이미지를 빌드할 수 있습니다. `docker build` 명령을 사용하여 `latest` 태그로 태그를 지정하여 이미지를 빌드합니다.

```
$ docker build -t my-spring-boot-app:latest .
```

## 쿠버네티스에 배포

Kubernetes는 널리 사용되는 컨테이너 오케스트레이션 플랫폼입니다. 컨테이너 그룹을 단일 단위로 관리하는 데 사용할 수 있습니다.

Spring Boot 애플리케이션을 Kubernetes에 배포하려면 먼저 '배포'를 생성해야 합니다. '배포'는 동일한 포드 그룹을 정의하고 특정 개수의 포드가 항상 실행되도록 합니다.

프로젝트의 루트 디렉토리에 `deployment.yaml` 파일을 생성합니다.

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

이 파일에서 복제본 수가 3인 'Deployment'를 정의했습니다. 또한 'Deployment'가 관리할 포드를 지정하는 'selector' 및 'template'도 정의했습니다.

이제 `kubectl` 명령줄 도구를 사용하여 Kubernetes에서 `Deployment`를 생성할 수 있습니다.

```
$ kubectl apply -f deployment.yaml
```

## Docker Swarm에 배포

Docker Swarm은 Docker의 컨테이너 오케스트레이션 플랫폼입니다. Docker 컨테이너 그룹을 단일 단위로 관리하는 데 사용할 수 있습니다.

Spring Boot 애플리케이션을 Docker Swarm에 배포하려면 먼저 `Stack`을 생성해야 합니다. '스택'은 함께 배포되는 서비스 그룹입니다.

프로젝트의 루트 디렉토리에 `stack.yaml` 파일을 생성합니다.

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

이 파일에서 `my-spring-boot-app`이라는 단일 서비스로 `Stack`을 정의했습니다. 또한 이 서비스의 복제본 3개를 배포하도록 지정했습니다.

이제 `docker stack` 명령을 사용하여 `Stack`을 Docker Swarm에 배포할 수 있습니다.

```
$ docker stack deploy -c stack.yaml my-spring-boot-app
```

## 추가 정보

- 쿠버네티스를 사용하는 경우 '서비스'를 만들어 애플리케이션을 외부에 노출할 수도 있습니다.
- Docker Swarm을 사용하는 경우 '네트워크'를 생성하여 서비스 간 통신을 허용할 수도 있습니다.

## 추가 자료

- [Spring Boot 참조 문서 - Spring Boot 애플리케이션 컨테이너화](https://docs.spring.io/spring-boot/docs/current/reference/html/deploying-spring-boot.html# deploying-spring-boot-containerizing )
- [Kubernetes 문서 - 배포 만들기](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/# creating-a-deployment)
- [Docker 설명서 - Swarm에 스택 배포](https://docs.docker.com/engine/reference/commandline/stack_deploy/# deploy-a-stack-to-a-swarm)