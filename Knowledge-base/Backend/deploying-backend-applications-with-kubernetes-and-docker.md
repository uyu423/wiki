---
title: Kubernetes 및 Docker를 사용하여 백엔드 애플리케이션 배포
description: 
published: true
date: 2023-02-01T04:36:56.751Z
tags: 
editor: markdown
dateCreated: 2023-02-01T04:36:55.107Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Deploying Backend Applications with Kubernetes and Docker***English** version of this document is available*](/en/Knowledge-base/Backend/deploying-backend-applications-with-kubernetes-and-docker)
{.links-list}



# 쿠버네티스와 도커로 백엔드 애플리케이션 배포하기

이 기사에서는 Kubernetes 및 Docker를 사용하여 백엔드 애플리케이션을 배포하는 방법을 다룹니다. 먼저 이러한 기술이 무엇이고 어떻게 함께 작동하는지 살펴보겠습니다. 그런 다음 Kubernetes 클러스터를 설정하고 여기에 애플리케이션을 배포하는 방법에 대한 단계별 가이드를 제공합니다.

## 쿠버네티스란?

Kubernetes는 개발자가 컨테이너화된 애플리케이션을 대규모로 배포하고 관리할 수 있도록 하는 컨테이너 오케스트레이션 플랫폼입니다. Kubernetes는 컨테이너화된 애플리케이션의 프로비저닝, 확장 및 모니터링을 자동화합니다. 또한 복잡한 애플리케이션을 쉽게 배포하고 관리할 수 있는 선언적 구성 모델을 제공합니다.

## 도커란?

Docker는 개발자가 격리된 환경에서 애플리케이션을 패키징하고 배포할 수 있도록 하는 컨테이너화 플랫폼입니다. Docker 컨테이너는 애플리케이션을 위한 경량의 휴대용 독립형 환경을 제공합니다. 배포하기 쉽고 Docker를 지원하는 모든 플랫폼에서 실행할 수 있습니다.

## Kubernetes와 Docker는 어떻게 함께 작동합니까?

Kubernetes와 Docker는 함께 작동하여 컨테이너화된 애플리케이션을 배포하고 관리하기 위한 플랫폼을 제공합니다. Kubernetes는 Docker 컨테이너의 프로비저닝, 확장 및 모니터링을 자동화합니다. 또한 복잡한 애플리케이션을 쉽게 배포하고 관리할 수 있는 선언적 구성 모델을 제공합니다.

## Kubernetes 클러스터 설정

이 섹션에서는 Kubernetes 클러스터를 설정하는 방법을 설명합니다. Kubernetes 명령줄 도구인 kubectl을 사용하여 클러스터를 설정합니다.

먼저 kubectl을 설치해야 합니다. 우리는 이것을 curl로 할 수 있습니다:

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

다음으로 kubectl 바이너리를 실행 가능하게 만들어야 합니다.

```
chmod +x ./kubectl
```

마지막으로 kubectl 바이너리를 PATH로 옮길 수 있습니다.

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

이제 kubectl을 설치했으므로 이를 사용하여 Kubernetes 클러스터를 설정할 수 있습니다. 단일 노드에서 실행되는 Kubernetes 구현인 Minikube를 사용합니다.

먼저 Minikube를 설치해야 합니다. 우리는 이것을 curl로 할 수 있습니다:

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

다음으로 Minikube 바이너리를 실행 가능하게 만들어야 합니다.

```
chmod +x minikube
```

마지막으로 Minikube 바이너리를 PATH로 옮길 수 있습니다.

```
sudo mv minikube /usr/local/bin/
```

이제 Minikube를 설치했으므로 이를 사용하여 Kubernetes 클러스터를 설정할 수 있습니다. Minikube 클러스터를 시작하려면 다음 명령을 실행합니다.

```
minikube start
```

그러면 하나의 노드로 Minikube 클러스터가 시작됩니다.

## Kubernetes에 애플리케이션 배포

이 섹션에서는 애플리케이션을 Kubernetes에 배포하는 방법을 다룹니다. 간단한 Node.js 애플리케이션을 예로 사용하겠습니다.

먼저 애플리케이션을 위한 Dockerfile을 생성해야 합니다. Dockerfile은 Docker 이미지를 빌드하기 위한 지침이 포함된 텍스트 파일입니다.

Dockerfile은 다음과 같습니다.

```
FROM node:8

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

이 Dockerfile은 node:8 Docker 이미지를 기본 이미지로 사용합니다. 그런 다음 프로젝트에서 package.json 및 package-lock.json 파일을 /app 디렉터리로 복사합니다. 다음으로 npm install을 실행하여 종속성을 설치합니다. 마지막으로 나머지 프로젝트 파일을 /app 디렉터리에 복사하고 포트 3000을 노출합니다.

이제 Dockerfile이 있으므로 Docker 이미지를 빌드할 수 있습니다. 이미지 이름을 my-app로 지정합니다.

```
docker build -t my-app .
```

이렇게 하면 my-app이라는 이름의 Docker 이미지가 빌드됩니다.

이제 Docker 이미지가 있으므로 Docker 레지스트리로 푸시할 수 있습니다. Docker Hub를 레지스트리로 사용합니다.

먼저 Docker Hub 계정을 만들어야 합니다. 그런 다음 Docker Hub 계정에 로그인해야 합니다.

```
docker login
```

다음으로 Docker Hub 사용자 이름으로 Docker 이미지에 태그를 지정해야 합니다.

```
docker tag my-app <your-docker-hub-username>/my-app
```

마지막으로 Docker 이미지를 Docker Hub로 푸시할 수 있습니다.

```
docker push <your-docker-hub-username>/my-app
```

이제 Docker 이미지가 Docker Hub에 있으므로 이를 Kubernetes 클러스터에 배포할 수 있습니다.

먼저 배포를 생성해야 합니다. 배포는 복제본 그룹을 관리하는 Kubernetes 개체입니다. 복제본은 Kubernetes가 우리 노드에서 실행할 애플리케이션의 복사본입니다.

배포를 만들려면 다음 명령을 실행합니다.

```
kubectl create deployment my-app --image=<your-docker-hub-username>/my-app
```

이렇게 하면 my-app이라는 배포가 생성됩니다. --image 플래그는 배포에서 사용할 Docker 이미지를 지정합니다.

다음으로 서비스를 만들어야 합니다. 서비스는 애플리케이션을 외부 세계에 노출하는 Kubernetes 개체입니다.

서비스를 생성하려면 다음 명령을 실행합니다.

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=3000
```

이렇게 하면 my-app이라는 서비스가 생성됩니다. --type 플래그는 서비스 유형을 지정합니다. --port 플래그는 서비스에서 사용할 포트를 지정합니다. --target-port 플래그는 애플리케이션이 실행되는 포트를 지정합니다.

마지막으로 서비스의 URL을 얻을 수 있습니다.

```
kubectl get service my-app
```

이것은 우리 서비스의 URL을 출력합니다. 이제 이 URL에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 Kubernetes 및 Docker를 사용하여 백엔드 애플리케이션을 배포하는 방법을 다루었습니다. 먼저 이러한 기술이 무엇이고 어떻게 함께 작동하는지 살펴보았습니다. 그런 다음 Kubernetes 클러스터를 설정하고 여기에 애플리케이션을 배포하는 방법에 대한 단계별 가이드를 제공했습니다.