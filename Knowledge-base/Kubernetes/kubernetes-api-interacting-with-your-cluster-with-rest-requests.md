---
title: Kubernetes API: REST 요청으로 클러스터와 상호 작용
description: 
published: true
date: 2023-02-14T03:33:33.290Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:33:30.961Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes API: Interacting with Your Cluster with REST Requests***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-api-interacting-with-your-cluster-with-rest-requests)
{.links-list}


# Kubernetes API: REST 요청으로 클러스터와 상호 작용

이 기사에서는 Kubernetes API를 사용하여 Kubernetes 클러스터와 상호 작용하는 방법을 살펴보겠습니다. Kubernetes API에 대한 REST 요청 작성의 기본 사항을 다루고 가장 일반적인 API 리소스 및 작업 중 일부를 살펴보겠습니다.

## REST 요청하기

Kubernetes API는 [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) API이므로 모든 HTTP 클라이언트를 사용하여 API에 요청할 수 있습니다. 적절한 API 엔드포인트에 HTTP 요청을 보내기만 하면 Kubernetes API가 요청된 데이터로 응답합니다.

Kubernetes API에 요청하려면 호출하려는 API 끝점의 URL을 알아야 하고 사용할 HTTP 메서드를 지정해야 합니다. 가장 일반적인 HTTP 메서드는 `GET`, `POST`, `PUT` 및 `DELETE`입니다.

예를 들어 네임스페이스의 모든 포드 목록을 가져오려면 `/api/v1/namespaces/{namespace}/pods` 엔드포인트에 `GET` 요청을 합니다. 새 포드를 만들려면 동일한 엔드포인트에 대해 'POST' 요청을 합니다.

URL 및 HTTP 메서드 외에도 `Bearer {token}` 값을 사용하여 `Authorization`이라는 [HTTP 헤더](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)를 지정해야 합니다. 여기서 `{token}`은 유효한 Kubernetes API 토큰입니다. `kubectl get secrets` 명령을 실행하여 Kubernetes API 토큰을 얻을 수 있습니다.

## 공통 API 리소스

이제 Kubernetes API에 대한 REST 요청의 기본 사항을 다루었으므로 가장 일반적인 API 리소스 중 일부를 살펴보겠습니다.

### 포드

포드는 Kubernetes에서 배포 가능한 가장 작은 단위이며 항상 동일한 노드에 함께 배치되고 함께 예약됩니다. 포드는 애플리케이션의 단일 인스턴스를 나타내며 하나 이상의 컨테이너를 포함할 수 있습니다.

네임스페이스의 모든 포드 목록을 가져오려면 `/api/v1/namespaces/{namespace}/pods` 엔드포인트에 `GET` 요청을 할 수 있습니다. 특정 팟(Pod)의 세부사항을 가져오려면 `/api/v1/namespaces/{namespace}/pods/{name}` 엔드포인트에 `GET` 요청을 할 수 있습니다.

새 포드를 생성하려면 `/api/v1/namespaces/{namespace}/pods` 엔드포인트에 `POST` 요청을 할 수 있습니다. 요청 본문은 포드 사양을 지정하는 [JSON](https://www.json.org/) 또는 [YAML](https://yaml.org/) 객체여야 합니다.

다음은 JSON으로 된 포드 사양의 예입니다.

```json
{
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "nginx-pod",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "nginx",
        "image": "nginx:1.7.9",
        "ports": [
          {
            "containerPort": 80
          }
        ]
      }
    ]
  }
}
```

YAML의 동일한 사양은 다음과 같습니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
```

포드를 업데이트하려면 `/api/v1/namespaces/{namespace}/pods/{name}` 엔드포인트에 대해 `PUT` 또는 `PATCH` 요청을 할 수 있습니다. 요청 본문은 포드 사양을 지정하는 JSON 또는 YAML 개체여야 합니다.

포드를 삭제하려면 `/api/v1/namespaces/{namespace}/pods/{name}` 엔드포인트에 대해 `DELETE` 요청을 할 수 있습니다.

### 복제 세트

레플리카 세트는 지정된 수의 포드 레플리카가 항상 실행되도록 하는 [Kubernetes 리소스](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)입니다. 포드가 삭제되거나 충돌하는 경우 레플리카 세트는 이를 대체할 새 포드가 생성되도록 합니다.

네임스페이스의 모든 복제 세트 목록을 가져오려면 `/apis/apps/v1/namespaces/{namespace}/replicasets` 엔드포인트에 `GET` 요청을 할 수 있습니다. 특정 복제본 세트의 세부 정보를 가져오려면 `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` 엔드포인트에 대해 `GET` 요청을 할 수 있습니다.

새 복제 세트를 생성하려면 `/apis/apps/v1/namespaces/{namespace}/replicasets` 엔드포인트에 `POST` 요청을 할 수 있습니다. 요청 본문은 복제 세트 사양을 지정하는 JSON 또는 YAML 객체여야 합니다.

다음은 JSON 형식의 복제본 세트 사양의 예입니다.

```json
{
  "apiVersion": "apps/v1",
  "kind": "ReplicaSet",
  "metadata": {
    "name": "nginx-replicaset",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

YAML의 동일한 사양은 다음과 같습니다.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

레플리카 세트를 업데이트하려면 `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` 엔드포인트에 대해 `PUT` 또는 `PATCH` 요청을 할 수 있습니다. 요청 본문은 복제 세트 사양을 지정하는 JSON 또는 YAML 객체여야 합니다.

레플리카 세트를 삭제하려면 `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` 엔드포인트에 대해 `DELETE` 요청을 할 수 있습니다.

### 배포

[배포](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)는 레플리카 세트를 관리하고 포드의 원하는 상태를 지정하는 선언적 방법을 제공하는 상위 수준 리소스입니다. 배포는 복제본 세트를 정의하고 지정된 수의 복제본이 항상 실행되도록 합니다.

네임스페이스의 모든 배포 목록을 가져오려면 `/apis/apps/v1/namespaces/{namespace}/deployments` 엔드포인트에 `GET` 요청을 할 수 있습니다. 특정 배포에 대한 세부 정보를 가져오려면 `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` 엔드포인트에 대해 `GET` 요청을 할 수 있습니다.

새 배포를 만들려면 `/apis/apps/v1/namespaces/{namespace}/deployments` 엔드포인트에 대해 `POST` 요청을 할 수 있습니다. 요청 본문은 배포 사양을 지정하는 JSON 또는 YAML 개체여야 합니다.

다음은 JSON으로 된 배포 사양의 예입니다.

```json
{
  "apiVersion": "apps/v1",
  "kind": "Deployment",
  "metadata": {
    "name": "nginx-deployment",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

YAML의 동일한 사양은 다음과 같습니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

배포를 업데이트하려면 `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` 엔드포인트에 대해 `PUT` 또는 `PATCH` 요청을 할 수 있습니다. 요청 본문은 배포 사양을 지정하는 JSON 또는 YAML 개체여야 합니다.

배포를 삭제하려면 `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` 엔드포인트에 대해 `DELETE` 요청을 할 수 있습니다.

## 결론

이 기사에서는 REST 요청을 사용하여 Kubernetes API와 상호 작용하는 기본 사항을 다뤘습니다. 가장 일반적인 API 리소스 중 일부를 살펴보고 Kubernetes API를 사용하여 해당 리소스를 생성, 읽기, 업데이트 및 삭제하는 방법을 살펴보았습니다.