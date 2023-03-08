---
title: Kubernetes 확장 API: 클러스터의 기능 향상
description: 
published: true
date: 2023-02-17T18:17:22.513Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:23:22.397Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kubernetes Extension APIs: Enhancing the Functionality of Your Cluster***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}



# Kubernetes 확장 API: 클러스터의 기능 향상

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 시스템입니다. 애플리케이션을 구성하는 컨테이너를 논리 단위로 그룹화하여 쉽게 관리하고 검색할 수 있습니다. Kubernetes는 스토리지 오케스트레이션, 네트워킹 및 보안을 위한 메커니즘도 제공합니다.

Kubernetes 기능 확장은 인기 있는 주제이며 이를 수행하는 방법에는 여러 가지가 있습니다. 이 기사에서는 Kubernetes Extension API에 중점을 둘 것입니다. 그것들이 무엇인지, 어떻게 작동하는지, 왜 사용해야 하는지에 대해 논의할 것입니다. 또한 시작할 수 있도록 몇 가지 샘플 코드를 제공합니다.

## Kubernetes 확장 API란 무엇인가요?

Kubernetes Extension API는 Kubernetes 클러스터의 기능을 확장할 수 있는 API 세트입니다. 핵심 코드를 변경하지 않고 Kubernetes에 새로운 기능을 추가하는 방법을 제공합니다.

확장 API는 CRD(CustomResourceDefinitions)로 구현됩니다. CRD는 Kubernetes에 새 리소스를 추가하는 방법입니다. 리소스는 Pod 또는 서비스와 같이 Kubernetes에서 관리할 수 있는 개체입니다. CRD를 사용하면 Kubernetes가 관리할 수 있는 새 리소스를 정의할 수 있습니다.

## Kubernetes Extension API는 어떻게 작동하나요?

Kubernetes Extension API는 CRD(CustomResourceDefinitions)로 구현됩니다. CRD는 Kubernetes에 새 리소스를 추가하는 방법입니다. 리소스는 Pod 또는 서비스와 같이 Kubernetes에서 관리할 수 있는 개체입니다. CRD를 사용하면 Kubernetes가 관리할 수 있는 새 리소스를 정의할 수 있습니다.

각 CRD에는 이름, 유형 및 속성을 포함하여 리소스에 대한 설명이 있습니다. Kubernetes는 이 정보를 사용하여 새 리소스를 생성합니다. 그런 다음 Kubernetes API를 사용하여 이 새 리소스를 관리할 수 있습니다.

## Kubernetes Extension API를 사용하는 이유는 무엇입니까?

Kubernetes Extension API는 핵심 코드를 변경하지 않고 Kubernetes에 새로운 기능을 추가하는 방법을 제공합니다. 이는 새 기능을 추가하려는 경우 또는 클러스터의 안정성에 영향을 주지 않고 새 코드를 실험하려는 경우에 유용할 수 있습니다.

확장 API는 Kubernetes 커뮤니티와 코드를 공유하는 방법도 제공합니다. 코드가 다른 사람에게 유용하다고 생각되면 Kubernetes에 포함되도록 제출할 수 있습니다.

## 샘플 코드

다음은 CustomResourceDefinition의 간단한 예입니다.

```
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: mycrd.example.com
spec:
  scope: Cluster
  group: example.com
  version: v1
  names:
    plural: mycrds
    singular: mycrd
    kind: MyCrd
    shortNames:
    - crd
  validation:
    openAPIV3Schema:
      description: MyCrds are ..."
      type: object
      properties:
        spec:
          type: object
          properties:
            size:
              type: integer
              minimum: 1
              maximum: 100
          required:
          - size
  subresources:
    status: {}
```

이 CRD는 "MyCrd"라는 리소스를 정의합니다. 이 리소스에는 1에서 100 사이의 정수인 "크기"라는 속성이 있습니다.

Kubernetes API를 사용하여 MyCrds를 생성, 업데이트 및 삭제할 수 있습니다.

```
# Create a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 10

# Update a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 20

# Delete a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 0
```

## 결론

Kubernetes Extension API는 핵심 코드를 변경하지 않고 Kubernetes에 새로운 기능을 추가하는 방법을 제공합니다. Kubernetes에 새 리소스를 추가하는 방법인 CRD(CustomResourceDefinitions)로 구현됩니다. 각 CRD에는 이름, 유형 및 속성을 포함하여 리소스에 대한 설명이 있습니다. Kubernetes는 이 정보를 사용하여 새 리소스를 생성합니다.

Kubernetes Extension API를 사용하여 Kubernetes에 새 기능을 추가하거나 클러스터의 안정성에 영향을 주지 않고 새 코드를 실험할 수 있습니다. 코드가 다른 사람에게 유용하다고 생각되면 Kubernetes에 포함되도록 제출할 수 있습니다.