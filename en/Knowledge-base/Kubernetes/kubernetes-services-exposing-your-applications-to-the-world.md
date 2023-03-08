---
title: Kubernetes Services: Exposing Your Applications to the World
description: 
published: true
date: 2023-02-06T08:55:31.990Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:55:26.487Z
---

- [Servicios de Kubernetes: exposición de sus aplicaciones al mundo***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}
- [Kubernetes 服务：向世界公开您的应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}
- [Kubernetes Services: 애플리케이션을 전 세계에 노출***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}


# Kubernetes Services: Exposing Your Applications to the World

In a traditional deployment, when you want to expose a new service to the world, you would have to update your firewall rules to allow traffic to reach your new service. In a containerized deployment using Kubernetes, you can use a `Service` object to expose your applications to the world.

A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them - sometimes called a micro-service. Each Service is assigned a unique IP address (sometimes called the “cluster IP”), which is used by the Service proxies (see below) and is part of any URLs used to access the Service.

There are two types of Services in Kubernetes: `ClusterIP` and `NodePort`.

`ClusterIP` Services, the default Kubernetes Service type, expose the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.

`NodePort` Services expose the Service on the same port of each Node in the cluster. This type makes the Service reachable from outside the cluster on each Node's IP at a static port (the `NodePort`). You can use `NodePort` Services to expose an application running in a Kubernetes cluster to the internet.

In this article, we will focus on `NodePort` Services.

## Creating a Service

Let's say we have a deployment with two Pods, each running a simple web server on port 8080. We can expose these Pods to the world with a `NodePort` Service like this:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
```

In this example, we've defined a Service named `my-service` which selects Pods with the `app` label set to `my-app`. We've also defined that the Service should expose port 80 (the `port`) and forward traffic to port 8080 on the selected Pods (the `targetPort`).

## Accessing the Service

Once you've created a Service, you can access it from outside the cluster on each Node's IP at the `NodePort`:

```
http://<Node IP>:<NodePort>
```

For example, if we have a Service with a `NodePort` of 31001, we can access it at:

```
http://<Node IP>:31001
```

## Conclusion

In this article, we've seen how to use `NodePort` Services to expose applications running in a Kubernetes cluster to the internet. We've seen how to create a Service and how to access it from outside the cluster.