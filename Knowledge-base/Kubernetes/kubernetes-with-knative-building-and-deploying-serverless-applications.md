---
title: Knative를 사용한 Kubernetes: 서버리스 애플리케이션 구축 및 배포
description: 
published: true
date: 2023-02-12T02:17:42.614Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:17:36.014Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with Knative: Building and Deploying Serverless Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-knative-building-and-deploying-serverless-applications)
{.links-list}


# Knative를 사용한 Kubernetes: 서버리스 애플리케이션 구축 및 배포

이 기사에서는 Kubernetes를 Knative와 함께 사용하여 서버리스 애플리케이션을 빌드하고 배치하는 방법을 살펴봅니다. 서버리스 컴퓨팅 및 Kubernetes에 대한 간략한 개요부터 시작하여 Knative가 Kubernetes 에코시스템에 어떻게 적용되는지 살펴보겠습니다. 그런 다음 Kubernetes 및 Knative를 사용하여 서버리스 애플리케이션을 구축하고 배포하는 간단한 예를 살펴보겠습니다.

## 서버리스 컴퓨팅이란 무엇입니까?

서버리스 컴퓨팅은 클라우드 제공자가 서버를 운영하고 고객은 사용한 컴퓨팅 시간에 대해서만 비용을 지불하는 클라우드 컴퓨팅 실행 모델입니다. 서버리스 컴퓨팅은 필요에 따라 백엔드 서비스를 제공하는 방법입니다.

서버리스 컴퓨팅에는 두 가지 유형이 있습니다.

- FaaS(Function as a Service): 주문형으로 사용자 제공 코드를 실행하는 서비스.
- BaaS(Backend as a Service): 푸시 알림이나 스토리지와 같은 애플리케이션에 백엔드를 제공하는 서비스.

## 쿠버네티스란?

Kubernetes는 컨테이너화된 워크로드 및 서비스를 관리하기 위한 이식 가능하고 확장 가능한 오픈 소스 플랫폼으로, 선언적 구성과 자동화를 모두 용이하게 합니다. 그것은 크고 빠르게 성장하는 생태계를 가지고 있습니다. 호스팅된 Kubernetes 솔루션을 포함하여 Kubernetes 서비스, 지원 및 도구를 광범위하게 사용할 수 있습니다.

## 네이티브란?

Knative는 Kubernetes를 확장하여 서버리스 워크로드를 위한 플랫폼을 제공하는 오픈 소스 구성요소 세트입니다. Knative는 세 가지 구성 요소로 구성됩니다.

- 제공: HTTP 프록시 및 컴퓨팅 리소스 자동 확장을 포함하여 Kubernetes에서 서버리스 플랫폼을 제공하는 구성 요소 집합입니다.
- 빌드: 서버리스 컨테이너 이미지 빌드를 제공하는 구성 요소 집합입니다.
- Eventing: 이벤트 기반 메시징 및 스트리밍을 제공하는 구성 요소 집합입니다.

Knative는 Google Kubernetes Engine(GKE), Azure Kubernetes Service(AKS) 및 Amazon Elastic Container Service for Kubernetes(EKS)를 포함하여 Kubernetes를 실행할 수 있는 모든 컨테이너 오케스트레이터와 함께 작동하도록 설계되었습니다.

## Kubernetes에서 서버리스 애플리케이션 구축 및 배포

이 섹션에서는 Knative를 사용하여 Kubernetes에서 서버리스 애플리케이션을 구축하고 배포하는 예를 살펴보겠습니다. Go로 작성된 간단한 "Hello, World" 예제를 사용합니다.

먼저 다음 코드를 사용하여 `main.go`라는 파일을 만듭니다.

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

다음으로 다음 내용으로 `Dockerfile`을 만듭니다.

```
FROM golang:1.11

WORKDIR /go/src/app

COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["app"]
```

이제 코드와 `Dockerfile`이 있으므로 컨테이너 이미지를 빌드하고 컨테이너 레지스트리에 푸시할 수 있습니다.

```
$ docker build -t gcr.io/<project-id>/helloworld:v1 .
$ docker push gcr.io/<project-id>/helloworld:v1
```

`<project-id>`를 Google Cloud Platform 프로젝트 ID로 바꿉니다.

컨테이너 이미지가 레지스트리에 푸시되면 `kubectl` 명령을 사용하여 Kubernetes에 배포할 수 있습니다.

```
$ kubectl apply -f helloworld.yaml
```

여기서 `helloworld.yaml`은 다음 콘텐츠가 포함된 YAML 파일입니다.

```yaml
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: helloworld
  namespace: default
spec:
  template:
    spec:
      containers:
        - image: gcr.io/<project-id>/helloworld:v1
          env:
            - name: TARGET
              value: "World"
```

서비스가 배포되면 애플리케이션의 URL을 볼 수 있습니다.

```
$ kubectl get ksvc
NAME            URL                                                 LATESTCREATED          LATESTREADY             READY     REASON
helloworld      http://helloworld-default.default.svc.cluster.local   helloworld-00001-00000   helloworld-00001-00000   True
```

URL을 컬링하여 테스트할 수 있습니다.

```
$ curl http://helloworld-default.default.svc.cluster.local
Hello, World!
```

## 결론

이 기사에서는 Kubernetes를 Knative와 함께 사용하여 서버리스 애플리케이션을 빌드하고 배치하는 방법을 살펴보았습니다. 서버리스 컴퓨팅이 무엇인지, Knative가 Kubernetes 에코시스템에 어떻게 부합하는지 살펴보았습니다. 마지막으로 Kubernetes 및 Knative를 사용하여 서버리스 애플리케이션을 구축하고 배포하는 간단한 예를 살펴보았습니다.