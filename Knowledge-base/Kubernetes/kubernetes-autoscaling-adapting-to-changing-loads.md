---
title: Kubernetes Autoscaling: 변화하는 로드에 적응
description: 
published: true
date: 2023-02-08T18:32:37.150Z
tags: 
editor: markdown
dateCreated: 2023-02-08T18:32:30.794Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Autoscaling: Adapting to Changing Loads***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-autoscaling-adapting-to-changing-loads)
{.links-list}


# 쿠버네티스 오토스케일링: 부하 변화에 적응

조직이 마이크로서비스 아키텍처로 이동함에 따라 컨테이너화된 배포가 점차 인기를 얻고 있습니다. Kubernetes는 가장 널리 사용되는 컨테이너 오케스트레이션 플랫폼 중 하나이며 모든 규모의 조직에서 사용됩니다.

쿠버네티스의 핵심 기능 중 하나는 변화하는 로드에 대응하여 배포를 확장 또는 축소하는 기능입니다. 이를 자동 확장이라고 하며 새로운 기능이 출시되거나 트래픽이 급증하는 등 다양한 상황에서 유용할 수 있습니다.

이 기사에서는 Kubernetes에서 자동 크기 조정이 작동하는 방식과 이를 사용하여 변화하는 로드에 적응하는 방법을 살펴보겠습니다.

## 자동 크기 조정이란 무엇입니까?

자동 크기 조정은 변화하는 조건에 따라 시스템을 동적으로 확장 또는 축소하는 프로세스입니다. Kubernetes의 맥락에서 이는 일반적으로 배포의 복제본 수를 늘리거나 줄이는 것을 의미합니다.

AutoScaling은 CPU 사용률, 메모리 사용량 또는 기타 사용자 지정 메트릭의 변경에 따라 배포를 확장하는 데 사용할 수 있습니다. 보류 중인 포드 수 또는 사용 가능한 디스크 공간의 양에 따라 확장되도록 Kubernetes를 구성할 수도 있습니다.

## Kubernetes에서 자동 크기 조정은 어떻게 작동하나요?

Kubernetes의 자동 크기 조정은 복제 컨트롤러 또는 배포를 사용하여 달성됩니다. 복제 컨트롤러는 지정된 배포에 대해 원하는 수의 복제본을 유지 관리해야 합니다.

자동 크기 조정이 활성화되면 복제 컨트롤러는 원하는 수의 복제본을 유지하기 위해 필요에 따라 배포를 확장 또는 축소합니다. 복제본 수는 수동으로 지정하거나 CPU 사용률 또는 메모리 사용률과 같은 조건에 따라 자동으로 조정할 수 있습니다.

## 언제 자동 확장을 사용해야 하나요?

자동 크기 조정은 복제본 수를 동적으로 조정해야 하는 여러 상황에서 사용할 수 있습니다.

자동 확장의 몇 가지 일반적인 사용 사례는 다음과 같습니다.

- 트래픽 변화에 따라 배포 확장 또는 축소
- CPU 사용률 변화에 따라 배포 확장 또는 축소
- 메모리 사용량 변화에 따라 배포 확장 또는 축소

## Kubernetes에서 자동 확장을 활성화하는 방법

원하는 복제본 수를 지정하여 지정된 배포에 대해 자동 확장을 활성화할 수 있습니다. 이는 `kubectl` 명령줄 도구를 사용하거나 배포의 YAML 파일을 편집하여 수행할 수 있습니다.

`kubectl`을 사용하여 자동 크기 조정을 활성화하려면 `kubectl scale` 명령을 사용할 수 있습니다. 예를 들어 다음 명령은 배포에 원하는 복제본 수를 3으로 설정합니다.

```
kubectl scale --replicas=3 deployment/my-deployment
```

배포의 YAML 파일을 편집하여 자동 크기 조정을 활성화하려면 `spec` 섹션에 `replicas` 키를 추가해야 합니다. 예를 들어:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image
        ports:
        - containerPort: 8080
```

## 결론

이 기사에서는 Kubernetes에서 자동 크기 조정이 작동하는 방식과 이를 사용하여 변화하는 부하에 적응하는 방법을 살펴보았습니다. 자동 크기 조정을 사용하여 트래픽, CPU 사용률 또는 메모리 사용량의 변화에 따라 배포를 확장하거나 축소할 수 있습니다.

Kubernetes에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

- 쿠버네티스 공식 문서: https://kubernetes.io/docs/
- 쿠버네티스 커뮤니티 슬랙 채널: https://kubernetes.slack.com/
- CNCF 최종 사용자 커뮤니티 설문 조사 결과: https://www.cncf.io/blog/2019/03/12/cncf-end-user-community-survey-results/