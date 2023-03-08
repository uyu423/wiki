---
title: 075: Node.js를 사용하여 Kubernetes에 TensorFlow.js 애플리케이션 배포
description: 
published: true
date: 2023-02-03T00:17:49.268Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:17:44.588Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [075: Deploying TensorFlow.js Applications on Kubernetes with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/075-deploying-tensorflow-js-applications-on-kubernetes-with-node-js)
{.links-list}


# 075: Node.js로 Kubernetes에 TensorFlow.js 애플리케이션 배포

TensorFlow.js는 JavaScript에서 기계 학습을 위한 강력한 도구이며 Node.js는 서버 측 JavaScript 애플리케이션을 위한 인기 있는 런타임입니다. 이 게시물에서는 널리 사용되는 컨테이너 오케스트레이션 플랫폼인 Kubernetes에 TensorFlow.js 애플리케이션을 배포하는 방법을 보여줍니다.

Kubernetes는 컨테이너화된 애플리케이션을 대규모로 배포하기 위한 훌륭한 플랫폼입니다. 자동 확장, 로드 밸런싱 및 롤링 업데이트와 같은 기능을 제공하여 대규모 애플리케이션을 관리할 때 큰 도움이 될 수 있습니다.

Node.js는 서버 측 JavaScript 애플리케이션에 널리 사용되는 런타임입니다. 빠르고 라이브러리 및 도구의 대규모 생태계가 있습니다.

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. 이를 통해 브라우저 또는 Node.js에서 모델을 교육하고 배포할 수 있습니다.

Kubernetes에 TensorFlow.js 애플리케이션을 배포하는 것은 애플리케이션의 가용성과 성능을 개선하는 좋은 방법이 될 수 있습니다. Kubernetes는 자동 확장 및 로드 밸런싱과 같은 기능을 제공할 수 있으며 이는 대규모 애플리케이션을 관리할 때 큰 도움이 될 수 있습니다.

이 게시물에서는 Kubernetes에 TensorFlow.js 애플리케이션을 배포하는 방법을 보여줍니다. Kubernetes 및 TensorFlow.js에 대한 기본 지식이 있다고 가정합니다. Kubernetes를 처음 사용하는 경우 Kubernetes 101 게시물을 확인할 수 있습니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

- 쿠버네티스 클러스터. 없는 경우 Kubernetes 클러스터를 만드는 방법에 대한 가이드를 확인할 수 있습니다.
- TensorFlow.js 애플리케이션. 없는 경우 TensorFlow.js 애플리케이션을 만드는 방법에 대한 가이드를 확인할 수 있습니다.

## 애플리케이션 배포

Kubernetes 클러스터와 TensorFlow.js 애플리케이션이 있으면 Kubernetes에 애플리케이션을 배포할 수 있습니다.

Kubernetes 및 TensorFlow.js에 대한 기본 지식이 있다고 가정합니다. Kubernetes를 처음 사용하는 경우 Kubernetes 101 게시물을 확인할 수 있습니다.

애플리케이션을 배포하려면 Kubernetes 배포를 생성해야 합니다. 배포는 팟(Pod) 그룹의 원하는 상태를 설명하는 Kubernetes 객체입니다.

배포를 만들려면 배포를 설명하는 YAML 파일을 만들어야 합니다. 다음은 TensorFlow.js 애플리케이션의 배포를 설명하는 YAML 파일의 예입니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tfjs-deployment
spec:
  selector:
    matchLabels:
      app: tfjs-app
  replicas: 1
  template:
    metadata:
      labels:
        app: tfjs-app
    spec:
      containers:
      - name: tfjs-container
        image: <your-docker-image>
        ports:
        - containerPort: 3000
```

YAML 파일에서 컨테이너의 이미지를 지정해야 합니다. 이것은 TensorFlow.js 애플리케이션의 이미지여야 합니다.

YAML 파일이 있으면 다음 명령을 실행하여 배포를 만들 수 있습니다.

```
kubectl apply -f <your-yaml-file>
```

이렇게 하면 Kubernetes 클러스터에 배포가 생성됩니다. 배포는 TensorFlow.js 애플리케이션을 실행하는 포드를 생성합니다.

## 애플리케이션에 액세스하기

배포가 생성되면 서비스를 생성하여 애플리케이션에 액세스할 수 있습니다. 서비스는 Pod 그룹에 액세스할 수 있는 방법을 제공하는 Kubernetes 개체입니다.

서비스를 생성하려면 서비스를 설명하는 YAML 파일을 생성해야 합니다. 다음은 TensorFlow.js 애플리케이션의 서비스를 설명하는 YAML 파일의 예입니다.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: tfjs-service
spec:
  type: LoadBalancer
  selector:
    app: tfjs-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
```

YAML 파일에서 서비스에 대한 선택기를 지정해야 합니다. 배포의 라벨 선택기와 일치해야 합니다.

YAML 파일이 있으면 다음 명령을 실행하여 서비스를 생성할 수 있습니다.

```
kubectl apply -f <your-yaml-file>
```

이렇게 하면 Kubernetes 클러스터에 서비스가 생성됩니다. 서비스는 TensorFlow.js 애플리케이션을 실행 중인 포드에 액세스하는 방법을 제공합니다.

## 배포 삭제

배포가 완료되면 다음 명령어를 실행하여 삭제할 수 있습니다.

```
kubectl delete deployment tfjs-deployment
```

이렇게 하면 생성된 배포 및 포드가 삭제됩니다.