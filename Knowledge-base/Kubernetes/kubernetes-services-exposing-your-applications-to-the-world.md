---
title: Kubernetes Services: 애플리케이션을 전 세계에 노출
description: 
published: true
date: 2023-02-06T08:55:28.070Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:55:26.478Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Services: Exposing Your Applications to the World***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}


# 쿠버네티스 서비스: 애플리케이션을 전 세계에 노출

기존 배포에서 새 서비스를 전 세계에 공개하려면 트래픽이 새 서비스에 도달할 수 있도록 방화벽 규칙을 업데이트해야 합니다. Kubernetes를 사용하는 컨테이너화된 배포에서 'Service' 객체를 사용하여 애플리케이션을 전 세계에 노출할 수 있습니다.

쿠버네티스의 서비스는 포드의 논리적 집합과 이에 액세스하는 정책(마이크로 서비스라고도 함)을 정의하는 추상화입니다. 각 서비스에는 서비스 프록시(아래 참조)가 사용하고 서비스 액세스에 사용되는 URL의 일부인 고유한 IP 주소("클러스터 IP"라고도 함)가 할당됩니다.

쿠버네티스에는 `ClusterIP`와 `NodePort`라는 두 가지 유형의 서비스가 있습니다.

기본 Kubernetes 서비스 유형인 'ClusterIP' 서비스는 클러스터의 내부 IP에 서비스를 노출합니다. 이 유형을 사용하면 클러스터 내에서만 서비스에 연결할 수 있습니다.

`NodePort` 서비스는 클러스터에 있는 각 노드의 동일한 포트에서 서비스를 노출합니다. 이 유형은 정적 포트(`NodePort`)에서 각 노드의 IP에 있는 클러스터 외부에서 서비스에 도달할 수 있도록 합니다. 'NodePort' 서비스를 사용하여 Kubernetes 클러스터에서 실행 중인 애플리케이션을 인터넷에 노출할 수 있습니다.

이 기사에서는 `NodePort` 서비스에 중점을 둘 것입니다.

## 서비스 만들기

각각 포트 8080에서 간단한 웹 서버를 실행하는 두 개의 포드가 있는 배포가 있다고 가정해 보겠습니다. 다음과 같이 `NodePort` 서비스를 사용하여 이러한 포드를 전 세계에 노출할 수 있습니다.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
```

이 예에서는 `my-app`으로 설정된 `app` 레이블이 있는 포드를 선택하는 `my-service`라는 서비스를 정의했습니다. 또한 서비스가 포트 80(`port`)을 노출하고 선택된 포드(`targetPort`)의 포트 8080으로 트래픽을 전달하도록 정의했습니다.

## 서비스 이용하기

서비스를 만든 후에는 `NodePort`에서 각 노드의 IP에 있는 클러스터 외부에서 서비스에 액세스할 수 있습니다.

```
http://<Node IP>:<NodePort>
```

예를 들어 `NodePort`가 31001인 서비스가 있는 경우 다음에서 액세스할 수 있습니다.

```
http://<Node IP>:31001
```

## 결론

이 기사에서는 `NodePort` 서비스를 사용하여 Kubernetes 클러스터에서 실행 중인 애플리케이션을 인터넷에 노출하는 방법을 살펴보았습니다. 서비스를 생성하는 방법과 클러스터 외부에서 서비스에 액세스하는 방법을 살펴보았습니다.