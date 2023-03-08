---
title: Kubernetes 리소스 관리: Pod에 대한 제한 및 요청 설정
description: 
published: true
date: 2023-02-05T20:17:22.174Z
tags: 
editor: markdown
dateCreated: 2023-02-05T20:17:20.634Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Resource Management: Setting Limits and Requests for Your Pods***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-resource-management-setting-limits-and-requests-for-your-pods)
{.links-list}


# Kubernetes 리소스 관리: Pod에 대한 제한 및 요청 설정

프로덕션 환경에서는 애플리케이션이 사용하는 리소스를 제어할 수 있어야 합니다. 이는 많은 애플리케이션이 동일한 클러스터에서 실행될 수 있는 Kubernetes와 같은 컨테이너화된 환경에서 특히 중요합니다.

Kubernetes에서 이를 수행하는 두 가지 주요 방법은 제한 및 요청 설정입니다. 제한은 포드가 사용할 수 있는 최대 리소스 양을 정의하고 요청은 포드에 필요한 최소 리소스 양을 정의합니다.

이 기사에서는 포드에 대한 제한 및 요청을 설정하는 방법을 살펴보겠습니다. 또한 이러한 설정을 사용하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

## 제한 및 요청 설정 방법

제한 및 요청은 팟(Pod)에서 주석으로 설정됩니다. 포드를 생성할 때 설정하거나 나중에 kubectl annotate 명령을 사용하여 설정할 수 있습니다.

다음은 포드를 생성할 때 제한 및 요청을 설정하는 방법의 예입니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  annotations:
    "limits.cpu": "1",
    "requests.cpu": "0.5"
spec:
  containers:
  - name: mycontainer
    image: myimage
```

이 예에서는 1 CPU 제한과 0.5 CPU 요청을 설정합니다.

kubectl annotate 명령을 사용하여 이러한 주석을 설정할 수도 있습니다.

```
kubectl annotate pod mypod "limits.cpu=1" "requests.cpu=0.5"
```

## 모범 사례

제한 및 요청을 설정할 때 염두에 두어야 할 몇 가지 모범 사례가 있습니다.

* 각 리소스에 대한 제한과 요청을 모두 설정합니다. 제한만 설정하면 Kubernetes는 이를 적용하지 않습니다.
* 귀하의 요청이 귀하의 한도보다 적은지 확인하십시오. 그렇지 않으면 포드가 예약되지 않습니다.
* 요청과 한도를 최대한 비슷하게 설정하십시오. 이렇게 하면 팟(Pod)이 필요한 리소스를 확보하는 데 도움이 됩니다.
* 클러스터에서 설정한 기본 제한에 유의하십시오. 제한 및 요청을 설정하지 않으면 포드가 이러한 기본값을 사용합니다.

## 결론

이 기사에서는 포드에 대한 제한 및 요청을 설정하는 방법을 살펴보았습니다. 또한 이러한 설정을 사용하기 위한 몇 가지 모범 사례도 살펴보았습니다. 이러한 모범 사례를 따르면 필요한 것보다 더 많은 리소스를 사용하지 않고도 팟(Pod)이 필요한 리소스를 얻을 수 있습니다.