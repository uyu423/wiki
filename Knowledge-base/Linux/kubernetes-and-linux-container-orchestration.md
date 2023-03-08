---
title: Kubernetes 및 Linux 컨테이너 오케스트레이션
description: 
published: true
date: 2023-02-12T03:32:21.441Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:32:14.466Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes and Linux Container Orchestration***English** document is available*](/en/Knowledge-base/Linux/kubernetes-and-linux-container-orchestration)
{.links-list}


# 쿠버네티스란?

Kubernetes는 원래 Google에서 설계한 오픈 소스 컨테이너 오케스트레이션 플랫폼입니다. 이제 Cloud Native Computing Foundation에서 유지 관리합니다. 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하는 데 사용할 수 있습니다.

# 리눅스 컨테이너란?

Linux 컨테이너는 격리된 환경에서 애플리케이션 또는 서비스를 실행하는 데 필요한 모든 구성 요소가 포함된 소프트웨어 패키지입니다. 컨테이너는 Virtual Machines의 대안이며 향상된 리소스 활용, 이식성 및 보안과 같은 많은 이점을 제공할 수 있습니다.

# 쿠버네티스와 리눅스 컨테이너 오케스트레이션

Kubernetes는 여러 컨테이너를 관리하는 컨테이너 오케스트레이션에 자주 사용됩니다. 여기에는 컨테이너 배포, 확장 및 모니터링과 같은 작업이 포함될 수 있습니다. Linux 컨테이너는 Kubernetes와 함께 사용하여 가볍고 이식 가능한 애플리케이션 환경을 제공할 수 있습니다.

# 쿠버네티스 시작하기

호스팅된 솔루션을 사용하거나 자체 인프라에 설치하는 등 몇 가지 Kubernetes 설치 옵션이 있습니다. 개발 및 테스트 목적으로 Docker와 같은 Linux 컨테이너 플랫폼에서 실행할 수 있는 단일 노드 Kubernetes 클러스터를 사용할 수도 있습니다.

Kubernetes가 설치되면 애플리케이션 배포를 시작할 수 있습니다. 이렇게 하려면 Kubernetes 배포 파일을 만들어야 합니다. 이 파일에는 사용할 컨테이너 이미지, 복제본 수, 노출된 포트 등 애플리케이션에 대한 모든 필수 정보가 포함되어 있습니다.

다음은 간단한 PHP 애플리케이션에 대한 예제 배포 파일입니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-php-app
  labels:
    app: my-php-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-php-app
  template:
    metadata:
      labels:
        app: my-php-app
    spec:
      containers:
      - name: my-php-app
        image: php:7.2-apache
        ports:
        - containerPort: 80
```

이 파일은 다음 명령을 실행하여 애플리케이션을 배포하는 데 사용할 수 있습니다.

```
$ kubectl apply -f my-php-app.yaml
```

# 결론

Kubernetes는 컨테이너화된 애플리케이션을 관리하기 위한 강력한 도구입니다. 컨테이너의 배포, 확장 및 관리를 자동화하는 데 사용할 수 있습니다. Linux 컨테이너는 Kubernetes와 함께 사용하여 가볍고 이식 가능한 애플리케이션 환경을 제공할 수 있습니다.