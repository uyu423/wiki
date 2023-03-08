---
title: Kubernetes Ingress: Exposing Your Services with Custom URLs
description: 
published: true
date: 2023-02-08T21:32:23.132Z
tags: 
editor: markdown
dateCreated: 2023-02-08T21:32:16.713Z
---

- [Ingress de Kubernetes: exposición de sus servicios con URL personalizadas***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-ingress-exposing-your-services-with-custom-urls)
{.links-list}
- [Kubernetes Ingress：使用自定义 URL 公开您的服务***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-ingress-exposing-your-services-with-custom-urls)
{.links-list}
- [Kubernetes Ingress: 사용자 지정 URL로 서비스 노출***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-ingress-exposing-your-services-with-custom-urls)
{.links-list}


# Kubernetes Ingress: Exposing Your Services with Custom URLs

Kubernetes Ingress is a powerful way to expose your services to the world. With Ingress, you can create custom URLs for your services, which can be useful for a number of reasons.

For example, you might want to create a URL for your service that is easy to remember, or you might want to create a URL that is specific to a certain service.

In this article, we'll take a look at how to create Kubernetes Ingress resources, and we'll also look at some of the benefits of using Ingress.

## Creating an Ingress Resource

Creating an Ingress resource is simple. Just create a file called ingress.yaml with the following contents:

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /my-service
        backend:
          serviceName: my-service
          servicePort: 80
```

In the above example, we've created an Ingress resource that exposes the service my-service at the URL /my-service.

## Benefits of Ingress

There are a number of benefits to using Ingress.

First, Ingress allows you to create custom URLs for your services. This can be useful for a number of reasons. For example, you might want to create a URL for your service that is easy to remember, or you might want to create a URL that is specific to a certain service.

Second, Ingress allows you to load balance traffic between multiple services. This can be useful if you have multiple services that serve the same purpose.

Third, Ingress allows you to route traffic based on the hostname. This can be useful if you want to route traffic to different services based on the hostname.

Fourth, Ingress allows you to route traffic based on the path. This can be useful if you want to route traffic to different services based on the path.

Finally, Ingress allows you to secure your services with SSL/TLS. This can be useful if you want to ensure that traffic to your services is encrypted.

## Conclusion

In this article, we've looked at how to create Kubernetes Ingress resources, and we've also looked at some of the benefits of using Ingress.