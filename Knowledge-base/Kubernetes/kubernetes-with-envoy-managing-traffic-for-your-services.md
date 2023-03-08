---
title: Envoy를 사용한 Kubernetes: 서비스 트래픽 관리
description: 
published: true
date: 2023-02-12T23:17:36.031Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:17:34.224Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with Envoy: Managing Traffic for Your Services***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-envoy-managing-traffic-for-your-services)
{.links-list}


# Envoy를 사용한 Kubernetes: 서비스 트래픽 관리

마이크로서비스 아키텍처에서는 각 서비스가 고유한 URL을 갖는 것이 일반적입니다. 이로 인해 서비스 간에 트래픽을 라우팅하려고 할 때, 특히 로드 밸런싱이 관련된 경우 문제가 발생할 수 있습니다.

이 문제에 대한 한 가지 해결책은 리버스 프록시를 사용하는 것입니다. 리버스 프록시는 클라이언트와 웹 서버 사이에 있는 서버입니다. 클라이언트의 모든 요청을 가로채 적절한 서버로 전달합니다.

Envoy는 Kubernetes와 함께 사용할 수 있는 인기 있는 오픈 소스 리버스 프록시입니다. Kubernetes는 컨테이너화된 애플리케이션을 대규모로 배포하고 관리할 수 있는 컨테이너 오케스트레이션 플랫폼입니다.

Envoy는 Kubernetes 클러스터의 서비스 간에 트래픽을 라우팅하는 데 사용할 수 있습니다. 또한 서비스 간에 트래픽 부하를 분산하는 데 사용할 수 있습니다.

이 기사에서는 Kubernetes와 함께 Envoy를 사용하여 서비스의 트래픽을 관리하는 방법을 살펴봅니다.

## 특사 설정

Envoy는 애플리케이션 컨테이너와 함께 사이드카 컨테이너로 배포할 수 있습니다. Envoy에 권장되는 배포 모델입니다.

사이드카 컨테이너는 애플리케이션 컨테이너와 함께 배포되는 컨테이너입니다. 애플리케이션 컨테이너와 외부 세계 사이에 전용 네트워크 링크를 제공합니다.

Envoy를 사이드카 컨테이너로 배포하려면 Envoy 컨테이너와 애플리케이션 컨테이너를 모두 포함하는 Kubernetes 포드를 생성해야 합니다.

다음은 Envoy를 Nginx 컨테이너와 함께 사이드카 컨테이너로 배포하는 포드 정의의 예입니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
  - name: envoy
    image: envoyproxy/envoy:v1.5.0
    ports:
    - containerPort: 8001
    - containerPort: 8002
```

위의 Pod 정의에서 두 개의 컨테이너를 정의했습니다. 첫 번째 컨테이너는 Nginx 컨테이너입니다. 두 번째 컨테이너는 Envoy 컨테이너입니다.

또한 Envoy 컨테이너에 대해 두 개의 포트를 정의했습니다. 포트 8001은 Envoy가 HTTP 트래픽을 수신할 포트입니다. 포트 8002는 Envoy가 TCP 트래픽을 수신할 포트입니다.

## Envoy 구성

Envoy는 JSON 구성 파일을 사용하여 구성됩니다. 구성 파일은 수신 포트, 업스트림 및 경로를 정의합니다.

청취 포트는 Envoy가 들어오는 트래픽을 청취하는 포트입니다.

업스트림은 Envoy가 트래픽을 프록시할 업스트림 서비스입니다.

경로는 Envoy가 트래픽을 업스트림에 매핑하는 데 사용할 경로입니다.

다음은 Envoy 구성 파일의 예입니다.

```json
{
  "admin": {
    "access_log_path": "/tmp/admin_access.log",
    "address": {
      "socket_address": {
        "address": "127.0.0.1",
        "port_value": 8001
      }
    }
  },
  "static_resources": {
    "listeners": [
      {
        "name": "listener_0",
        "address": {
          "socket_address": {
            "address": "127.0.0.1",
            "port_value": 80
          }
        },
        "filter_chains": [
          {
            "filters": [
              {
                "name": "envoy.http_connection_manager",
                "config": {
                  "stat_prefix": "ingress_http",
                  "route_config": {
                    "virtual_hosts": [
                      {
                        "name": "service",
                        "domains": [
                          "*"
                        ],
                        "routes": [
                          {
                            "match": {
                              "prefix": "/"
                            },
                            "route": {
                              "cluster": "service"
                            }
                          }
                        ]
                      }
                    ]
                  },
                  "http_filters": [
                    {
                      "name": "envoy.router"
                    }
                  ]
                }
              }
            ]
          }
        ]
      }
    ],
    "clusters": [
      {
        "name": "service",
        "connect_timeout": "0.25s",
        "type": "strict_dns",
        "lb_policy": "round_robin",
        "hosts": [
          {
            "socket_address": {
              "address": "127.0.0.1",
              "port_value": 8002
            }
          }
        ]
      }
    ]
  }
}
```

위의 구성 파일에서 포트 80의 수신기와 업스트림 서비스용 클러스터를 정의했습니다. 또한 "/" 경로에서 업스트림 서비스로 트래픽을 매핑하는 경로를 정의했습니다.

## 엔보이 배치

Envoy는 Kubernetes DaemonSet를 사용하여 배포할 수 있습니다. DaemonSet는 Kubernetes 클러스터의 모든 노드에 실행 중인 Envoy 컨테이너의 복사본이 있는지 확인합니다.

다음은 DaemonSet 정의의 예입니다.

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: envoy
  labels:
    app: envoy
spec:
  selector:
    matchLabels:
      app: envoy
  template:
    metadata:
      labels:
        app: envoy
    spec:
      containers:
      - name: envoy
        image: envoyproxy/envoy:v1.5.0
        ports:
        - containerPort: 8001
        - containerPort: 8002
        env:
        - name: ENVOY_CONFIG
          value: /etc/envoy/envoy.json
        volumeMounts:
        - name: envoy-config
          mountPath: /etc/envoy
      volumes:
      - name: envoy-config
        configMap:
          name: envoy-config
```

위의 DaemonSet 정의에서 Envoy용 컨테이너와 Envoy 구성 파일용 볼륨을 정의했습니다. Envoy 구성 파일을 가리키는 환경 변수도 정의했습니다.

## 결론

이 기사에서는 Kubernetes와 함께 Envoy를 사용하여 서비스의 트래픽을 관리하는 방법을 살펴보았습니다. Envoy를 구성하고 배포하는 방법도 살펴보았습니다.