---
title: Kubernetes 네트워크 정책: Pod 간 통신 규칙 적용
description: 
published: true
date: 2023-02-09T02:32:30.767Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:32:29.221Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Network Policies: Enforcing Communication Rules Between Pods***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-network-policies-enforcing-communication-rules-between-pods)
{.links-list}


# Kubernetes 네트워크 정책: 포드 간 통신 규칙 적용

Kubernetes 네트워크 정책은 Pod 간에 통신 규칙을 적용하는 방법을 제공합니다. 기본적으로 Kubernetes 클러스터의 모든 포드는 서로 통신할 수 있습니다. 그러나 어떤 경우에는 특정 포드로만 통신을 제한하는 것이 바람직할 수 있습니다. 예를 들어 웹 서버와 데이터베이스 서버 간의 통신은 허용하지만 웹 서버와 응용 프로그램 서버 간의 통신은 허용하지 않을 수 있습니다.

네트워크 정책을 사용하여 서로 통신할 수 있는 포드를 지정하여 이를 달성할 수 있습니다. 네트워크 정책은 Kubernetes 리소스로 구현되며 YAML 또는 JSON을 사용하여 정의할 수 있습니다.

다음은 웹 서버와 데이터베이스 서버 간의 통신을 허용하지만 웹 서버와 애플리케이션 서버 간의 통신을 허용하지 않는 네트워크 정책의 예입니다.

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-db
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - protocol: TCP
      port: 3306
```

이 네트워크 정책은 `/etc/kubernetes/manifests` 디렉토리에 `allow-web-db.yaml`이라는 파일을 생성하여 네임스페이스에 적용할 수 있습니다.

네트워크 정책을 사용하여 특정 포드 간의 통신을 거부할 수도 있습니다. 예를 들어 다음 네트워크 정책은 웹 서버와 애플리케이션 서버 간의 모든 통신을 거부합니다.

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-web-app
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: app
    ports:
    - protocol: TCP
      port: 80
```

이 네트워크 정책은 `/etc/kubernetes/manifests` 디렉토리에 `deny-web-app.yaml`이라는 파일을 생성하여 네임스페이스에 적용할 수 있습니다.

다른 포드 간의 통신을 거부하면서 특정 포드 간의 통신을 허용하는 것도 가능합니다. 예를 들어 다음 네트워크 정책은 웹 서버와 데이터베이스 서버 간의 통신을 허용하지만 웹 서버와 애플리케이션 서버 간의 통신은 거부합니다.

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-db-deny-web-app
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - protocol: TCP
      port: 3306
  - from:
    - podSelector:
        matchLabels:
          role: app
    ports:
    - protocol: TCP
      port: 80
```

이 네트워크 정책은 `/etc/kubernetes/manifests` 디렉토리에 `allow-web-db-deny-web-app.yaml`이라는 파일을 생성하여 네임스페이스에 적용할 수 있습니다.

네트워크 정책은 매우 강력할 수 있으며 포드 간에 복잡한 통신 규칙을 구현하는 데 사용할 수 있습니다. 그러나 네트워크 정책은 팟(Pod)에 적절하게 레이블이 지정된 경우에만 작동한다는 점에 유의해야 합니다. 팟(Pod) 레이블 지정 방법에 대한 자세한 정보는 Kubernetes 문서를 참조하십시오.

## 외부 리소스

- [Kubernetes 네트워크 정책](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Labeling Pods](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)