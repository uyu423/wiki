---
title: 044: 쿠버네티스와 함께 Nest.js 사용하기
description: 
published: true
date: 2023-02-15T16:33:14.636Z
tags: 
editor: markdown
dateCreated: 2023-02-15T16:33:13.074Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [044: Using Nest.js with Kubernetes***English** document is available*](/en/Knowledge-base/Nest-js/Learning/044-using-nest-js-with-kubernetes)
{.links-list}


# 쿠버네티스와 함께 Nest.js 사용하기

Kubernetes는 강력한 컨테이너 오케스트레이션 도구이며 Nest.js는 널리 사용되는 Node.js 프레임워크입니다. 이 게시물에서는 Kubernetes와 함께 Nest.js를 사용하는 방법을 보여줍니다.

## 전제 조건

- 쿠버네티스 클러스터
- 텍스트 편집기

## Nest.js 설치

먼저 Nest.js를 설치해야 합니다. Node.js 패키지 관리자인 npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install -g @nestjs/cli
```

## Nest.js 프로젝트 생성

Nest.js가 설치되면 Nest.js CLI를 사용하여 새 프로젝트를 만들 수 있습니다.

```
nest new project-name
```

## Nest.js 프로젝트 실행

다음 명령을 사용하여 Nest.js 프로젝트를 실행할 수 있습니다.

```
npm run start
```

## Kubernetes에 Nest.js 프로젝트 배포

kubectl 명령줄 도구를 사용하여 Nest.js 프로젝트를 Kubernetes에 배포할 수 있습니다.

먼저 다음 내용으로 `nest-deployment.yaml`이라는 파일을 만들어야 합니다.

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

`YOUR_DOCKER_HUB_USERNAME`을 Docker Hub 사용자 이름으로 바꿉니다.

다음으로 Nest.js 프로젝트를 빌드하고 Docker Hub에 푸시해야 합니다.

```
docker build -t YOUR_DOCKER_HUB_USERNAME/nest .
docker push YOUR_DOCKER_HUB_USERNAME/nest
```

마지막으로 Nest.js 프로젝트를 Kubernetes에 배포할 수 있습니다.

```
kubectl apply -f nest-deployment.yaml
```

## Nest.js 애플리케이션에 액세스

Kubernetes 클러스터 IP 주소를 통해 Nest.js 애플리케이션에 액세스할 수 있습니다.

```
http://CLUSTER_IP:8080
```

'CLUSTER_IP'를 Kubernetes 클러스터의 IP 주소로 바꿉니다.

## 결론

이 게시물에서는 Kubernetes와 함께 Nest.js를 사용하는 방법을 보여주었습니다. Nest.js를 설치하고 새 프로젝트를 생성하여 Kubernetes에 배포했습니다. 또한 Kubernetes 클러스터 IP 주소를 통해 Nest.js 애플리케이션에 액세스하는 방법도 보여 주었습니다.