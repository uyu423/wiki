---
title: Kubernetes Ingress: 사용자 지정 URL로 서비스 노출
description: 
published: true
date: 2023-02-08T21:32:18.537Z
tags: 
editor: markdown
dateCreated: 2023-02-08T21:32:16.706Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Ingress: Exposing Your Services with Custom URLs***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-ingress-exposing-your-services-with-custom-urls)
{.links-list}


# Kubernetes Ingress: 사용자 지정 URL로 서비스 노출

Kubernetes Ingress는 서비스를 전 세계에 노출하는 강력한 방법입니다. Ingress를 사용하면 서비스에 대한 사용자 정의 URL을 생성할 수 있으며 이는 여러 가지 이유로 유용할 수 있습니다.

예를 들어 기억하기 쉬운 서비스 URL을 만들거나 특정 서비스에 특정한 URL을 만들 수 있습니다.

이 기사에서는 Kubernetes 인그레스 리소스를 생성하는 방법을 살펴보고 인그레스 사용의 이점에 대해서도 살펴보겠습니다.

## 인그레스 리소스 만들기

인그레스 리소스를 만드는 것은 간단합니다. 다음 내용으로 ingress.yaml이라는 파일을 생성하기만 하면 됩니다.

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /my-service
        backend:
          serviceName: my-service
          servicePort: 80
```

위의 예에서는 URL /my-service에서 my-service 서비스를 노출하는 Ingress 리소스를 만들었습니다.

## Ingress의 이점

Ingress를 사용하면 여러 가지 이점이 있습니다.

첫째, Ingress를 사용하면 서비스에 대한 사용자 지정 URL을 만들 수 있습니다. 이는 여러 가지 이유로 유용할 수 있습니다. 예를 들어 기억하기 쉬운 서비스 URL을 만들거나 특정 서비스에 특정한 URL을 만들 수 있습니다.

둘째, Ingress를 사용하면 여러 서비스 간에 트래픽 부하를 분산할 수 있습니다. 이는 동일한 목적을 제공하는 여러 서비스가 있는 경우에 유용할 수 있습니다.

셋째, Ingress를 사용하면 호스트 이름을 기반으로 트래픽을 라우팅할 수 있습니다. 이는 호스트 이름을 기반으로 트래픽을 다른 서비스로 라우팅하려는 경우에 유용할 수 있습니다.

넷째, Ingress를 사용하면 경로를 기반으로 트래픽을 라우팅할 수 있습니다. 이는 경로를 기반으로 트래픽을 다른 서비스로 라우팅하려는 경우에 유용할 수 있습니다.

마지막으로 Ingress를 사용하면 SSL/TLS로 서비스를 보호할 수 있습니다. 이는 서비스에 대한 트래픽이 암호화되었는지 확인하려는 경우에 유용할 수 있습니다.

## 결론

이 기사에서는 Kubernetes 인그레스 리소스를 생성하는 방법과 인그레스 사용의 이점에 대해서도 살펴보았습니다.