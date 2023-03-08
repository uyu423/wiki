---
title: Kubernetes 사용자 지정 리소스 정의: Kubernetes API 확장
description: 
published: true
date: 2023-02-01T08:24:13.578Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:24:12.122Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kubernetes Custom Resource Definitions: Extending the Kubernetes API***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-custom-resource-definitions-extending-the-kubernetes-api)
{.links-list}



# Kubernetes 사용자 지정 리소스 정의: Kubernetes API 확장

Kubernetes 사용자 지정 리소스 정의(CRD)는 사용자 정의 객체를 나타내는 새로운 리소스로 Kubernetes API를 확장하는 방법을 제공합니다. CRD를 사용하면 Kubernetes 관리자와 개발자가 Kubernetes API 서버를 수정하거나 코드를 작성하지 않고도 새 리소스를 만들고 사용할 수 있습니다.

이 기사에서는 CRD의 작동 방식과 이를 사용하여 Kubernetes API를 확장하는 방법을 살펴보겠습니다. 또한 CRD의 일부 사용 사례를 살펴보고 커뮤니티에서 개발한 몇 가지 예제 CRD를 살펴볼 것입니다.

## Kubernetes 사용자 지정 리소스 정의란 무엇입니까?

CRD(Custom Resource Definition)는 새로운 Kubernetes 리소스를 정의하는 방법입니다. CRD는 사용자 정의 개체를 나타내는 새 리소스로 Kubernetes API를 확장하는 데 사용됩니다. CRD를 사용하면 Kubernetes 관리자와 개발자가 Kubernetes API 서버를 수정하거나 코드를 작성하지 않고도 새 리소스를 만들고 사용할 수 있습니다.

CRD는 포드 및 서비스와 같은 기본 제공 Kubernetes 리소스와 유사합니다. 기본 제공 리소스와 마찬가지로 CRD에는 이름, 스키마 및 작업 집합(예: 만들기, 읽기, 업데이트 및 삭제)이 있습니다. 내장 리소스와 함께 CRD를 사용하여 새로운 복합 리소스를 생성할 수도 있습니다.

## Kubernetes 사용자 정의 리소스 정의는 어떻게 작동합니까?

CRD는 Kubernetes API 서버에 저장되며 Kubernetes API 서버에서 사용자 요청을 검증하고 처리하는 데 사용됩니다. CRD는 OpenAPI v3 사양을 사용하여 정의됩니다.

OpenAPI v3 사양은 RESTful API를 설명하기 위한 표준입니다. API의 구조, 수행할 수 있는 작업, 입력 및 출력 형식, 인증 방법을 정의합니다.

OpenAPI v3 사양은 Kubernetes API 서버에서 사용자 요청의 유효성을 검사하는 데 사용됩니다. 사용자가 Kubernetes API 서버에 요청을 보내면 Kubernetes API 서버는 OpenAPI v3 사양을 사용하여 요청의 유효성을 검사합니다. 요청이 유효한 경우 Kubernetes API 서버는 요청을 적절한 CRD로 전달합니다.

Kubernetes API 서버는 OpenAPI v3 사양을 사용하여 사용자 요청의 유효성을 검사합니다. 요청이 유효한 경우 Kubernetes API 서버는 요청을 적절한 CRD로 전달합니다.

## Kubernetes 사용자 정의 리소스 정의를 사용하면 어떤 이점이 있습니까?

CRD는 기존 API 개발 방식에 비해 여러 가지 이점이 있습니다.

- CRD를 사용하면 Kubernetes API 서버를 수정하거나 코드를 작성하지 않고도 새 리소스를 정의할 수 있습니다.
- CRD는 Kubernetes API 서버에 저장되며 Kubernetes API 서버에서 사용자 요청을 검증하고 처리하는 데 사용됩니다.
- CRD는 RESTful API를 설명하기 위한 표준인 OpenAPI v3 사양을 사용하여 정의됩니다.
- CRD는 내장 리소스와 함께 사용하여 새로운 복합 리소스를 생성할 수 있습니다.

## Kubernetes 사용자 지정 리소스 정의의 사용 사례는 무엇입니까?

CRD는 사용자 정의 개체를 나타내는 새 리소스로 Kubernetes API를 확장하는 데 사용할 수 있습니다. CRD를 사용하면 Kubernetes 관리자와 개발자가 Kubernetes API 서버를 수정하거나 코드를 작성하지 않고도 새 리소스를 만들고 사용할 수 있습니다.

CRD는 다음을 나타내는 새 리소스를 만드는 데 사용할 수 있습니다.

- 네임스페이스, 노드 및 포드와 같은 클러스터 객체.
- 배포, 서비스 및 인그레스와 같은 애플리케이션 객체.
- 고객 기록, 주문 기록 및 제품 기록과 같은 사용자 지정 개체.

## Kubernetes 사용자 정의 리소스 정의를 생성하려면 어떻게 해야 합니까?

CRD 생성은 2단계 프로세스입니다.

1. OpenAPI v3 사양을 사용하여 CRD를 정의합니다.
2. Kubernetes API 서버에 CRD를 등록합니다.

OpenAPI v3 사양은 RESTful API를 설명하기 위한 표준입니다. API의 구조, 수행할 수 있는 작업, 입력 및 출력 형식, 인증 방법을 정의합니다.

OpenAPI v3 사양은 Kubernetes API 서버에서 사용자 요청의 유효성을 검사하는 데 사용됩니다. 사용자가 Kubernetes API 서버에 요청을 보내면 Kubernetes API 서버는 OpenAPI v3 사양을 사용하여 요청의 유효성을 검사합니다. 요청이 유효한 경우 Kubernetes API 서버는 요청을 적절한 CRD로 전달합니다.

Kubernetes API 서버에 CRD를 등록하는 것은 2단계 프로세스입니다.

1. 다음 내용으로 crd.yaml이라는 파일을 생성합니다.

```yaml
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: {crd-name}
spec:
  group: {crd-group}
  version: {crd-version}
  names:
    kind: {crd-kind}
    plural: {crd-plural}
  scope: {crd-scope}
```

2. Kubernetes API 서버에 CRD를 등록합니다.

```
kubectl create -f crd.yaml
```

## Kubernetes 사용자 지정 리소스 정의를 어떻게 사용합니까?

CRD를 생성하면 이를 사용하여 새 리소스를 생성할 수 있습니다. 리소스 생성은 2단계 프로세스입니다.

1. OpenAPI v3 사양을 사용하여 리소스를 정의합니다.
2. kubectl create 명령을 사용하여 리소스를 생성합니다.

OpenAPI v3 사양은 RESTful API를 설명하기 위한 표준입니다. API의 구조, 수행할 수 있는 작업, 입력 및 출력 형식, 인증 방법을 정의합니다.

OpenAPI v3 사양은 Kubernetes API 서버에서 사용자 요청의 유효성을 검사하는 데 사용됩니다. 사용자가 Kubernetes API 서버에 요청을 보내면 Kubernetes API 서버는 OpenAPI v3 사양을 사용하여 요청의 유효성을 검사합니다. 요청이 유효한 경우 Kubernetes API 서버는 요청을 적절한 CRD로 전달합니다.

리소스 생성은 2단계 프로세스입니다.

1. OpenAPI v3 사양을 사용하여 리소스를 정의합니다.
2. kubectl create 명령을 사용하여 리소스를 생성합니다.

```
kubectl create -f {resource-definition.yaml}
```

## Kubernetes 사용자 지정 리소스 정의의 예는 무엇입니까?

다음은 커뮤니티에서 개발한 CRD의 예입니다.

- [Kubernetes 네임스페이스](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/namespaces.md)
- [쿠버네티스 노드](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/nodes.md)
- [Kubernetes 포드](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/pods.md)
- [쿠버네티스 서비스](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/services.md)
- [Kubernetes 배포](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/deployments.md)
- [Kubernetes 인그레스](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/ingresses.md)
- [쿠버네티스 작업](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/jobs.md)
- [Kubernetes CronJob](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/cronjobs.md)

## 결론

이 기사에서는 CRD의 작동 방식과 CRD를 사용하여 Kubernetes API를 확장하는 방법을 살펴보았습니다. 또한 CRD의 일부 사용 사례를 살펴보고 커뮤니티에서 개발한 몇 가지 예제 CRD를 살펴보았습니다.