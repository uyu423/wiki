---
title: Kubernetes with Envoy：管理服务的流量
description: 
published: true
date: 2023-02-12T23:17:35.801Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:17:34.223Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with Envoy: Managing Traffic for Your Services***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-envoy-managing-traffic-for-your-services)
{.links-list}


# Kubernetes with Envoy：管理服务的流量

在微服务架构中，每个服务都有自己唯一的 URL 是很常见的。这会在尝试在服务之间路由流量时产生问题，尤其是在涉及负载平衡时。

解决此问题的一种方法是使用反向代理。反向代理是位于客户端和 Web 服务器之间的服务器。它拦截来自客户端的所有请求并将它们转发到适当的服务器。

Envoy 是一种流行的开源反向代理，可以与 Kubernetes 结合使用。 Kubernetes 是一个容器编排平台，可让您大规模部署和管理容器化应用程序。

Envoy 可用于在 Kubernetes 集群中的服务之间路由流量。它还可以用于负载平衡服务之间的流量。

在本文中，我们将研究如何使用 Envoy 和 Kubernetes 来管理您的服务的流量。

## 设置特使

Envoy 可以与您的应用程序容器一起部署为边车容器。这是 Envoy 的推荐部署模型。

sidecar 容器是与您的应用程序容器一起部署的容器。它在应用程序容器和外部世界之间提供专用网络链接。

要将 Envoy 部署为边车容器，您需要创建一个包含 Envoy 容器和您的应用程序容器的 Kubernetes Pod。

下面是一个示例 Pod 定义，它将 Envoy 部署为与 Nginx 容器一起的边车容器：

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

在上面的 Pod 定义中，我们定义了两个容器。第一个容器是我们的 Nginx 容器。第二个容器是 Envoy 容器。

我们还为 Envoy 容器定义了两个端口。端口 8001 是 Envoy 将侦听 HTTP 流量的端口。端口 8002 是 Envoy 将侦听 TCP 流量的端口。

## 配置特使

Envoy 使用 JSON 配置文件进行配置。配置文件定义监听端口、上游和路由。

侦听端口是 Envoy 将侦听传入流量的端口。

上游是 Envoy 将代理流量的上游服务。

路由是 Envoy 将用来将流量映射到上游的路由。

这是一个示例 Envoy 配置文件：

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

在上面的配置文件中，我们在端口 80 上定义了一个监听器，并为我们的上游服务定义了一个集群。我们还定义了一条路由，将流量从“/”路径映射到我们的上游服务。

## 部署特使

可以使用 Kubernetes DaemonSet 部署 Envoy。 DaemonSet 确保 Kubernetes 集群中的所有节点都有一个正在运行的 Envoy 容器副本。

下面是一个 DaemonSet 定义示例：

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

在上面的 DaemonSet 定义中，我们为 Envoy 定义了一个容器，为 Envoy 配置文件定义了一个卷。我们还定义了一个指向 Envoy 配置文件的环境变量。

## 结论

在本文中，我们研究了如何将 Envoy 与 Kubernetes 结合使用来管理您的服务的流量。我们还研究了如何配置和部署 Envoy。