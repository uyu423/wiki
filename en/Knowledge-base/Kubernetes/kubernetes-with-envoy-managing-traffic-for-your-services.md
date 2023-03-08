---
title: Kubernetes with Envoy: Managing Traffic for Your Services
description: 
published: true
date: 2023-02-12T23:17:41.455Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:17:34.232Z
---

- [Kubernetes con Envoy: administración del tráfico para sus servicios***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-envoy-managing-traffic-for-your-services)
{.links-list}
- [Kubernetes with Envoy：管理服务的流量***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-envoy-managing-traffic-for-your-services)
{.links-list}
- [Envoy를 사용한 Kubernetes: 서비스 트래픽 관리***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-envoy-managing-traffic-for-your-services)
{.links-list}


# Kubernetes with Envoy: Managing Traffic for Your Services

In a microservices architecture, it is common for each service to have its own unique URL. This can create problems when trying to route traffic between services, especially when load balancing is involved.

One solution to this problem is to use a reverse proxy. A reverse proxy is a server that sits between the client and the web server. It intercepts all requests from the client and forwards them to the appropriate server.

Envoy is a popular open source reverse proxy that can be used in conjunction with Kubernetes. Kubernetes is a container orchestration platform that enables you to deploy and manage containerized applications at scale.

Envoy can be used to route traffic between services in a Kubernetes cluster. It can also be used to load balance traffic between services.

In this article, we will look at how to use Envoy with Kubernetes to manage traffic for your services.

## Setting up Envoy

Envoy can be deployed as a sidecar container alongside your application container. This is the recommended deployment model for Envoy.

A sidecar container is a container that is deployed alongside your application container. It provides a dedicated network link between the application container and the outside world.

To deploy Envoy as a sidecar container, you need to create a Kubernetes Pod that contains both the Envoy container and your application container.

Here is an example Pod definition that deploys Envoy as a sidecar container alongside an Nginx container:

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

In the above Pod definition, we have defined two containers. The first container is our Nginx container. The second container is the Envoy container.

We have also defined two ports for the Envoy container. port 8001 is the port that Envoy will listen on for HTTP traffic. port 8002 is the port that Envoy will listen on for TCP traffic.

## Configuring Envoy

Envoy is configured using a JSON configuration file. The configuration file defines the listen ports, the upstreams, and the routes.

The listen ports are the ports that Envoy will listen on for incoming traffic.

The upstreams are the upstream services that Envoy will proxy traffic to.

The routes are the routes that Envoy will use to map traffic to the upstreams.

Here is an example Envoy configuration file:

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

In the above configuration file, we have defined a listener on port 80 and a cluster for our upstream service. We have also defined a route that maps traffic from the "/" path to our upstream service.

## Deploying Envoy

Envoy can be deployed using the Kubernetes DaemonSet. A DaemonSet ensures that all nodes in the Kubernetes cluster have a copy of the Envoy container running.

Here is an example DaemonSet definition:

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

In the above DaemonSet definition, we have defined a container for Envoy and a volume for the Envoy configuration file. We have also defined an environment variable that points to the Envoy configuration file.

## Conclusion

In this article, we have looked at how to use Envoy with Kubernetes to manage traffic for your services. We have also looked at how to configure and deploy Envoy.