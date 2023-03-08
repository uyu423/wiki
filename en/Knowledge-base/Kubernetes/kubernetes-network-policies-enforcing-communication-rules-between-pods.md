---
title: Kubernetes Network Policies: Enforcing Communication Rules Between Pods
description: 
published: true
date: 2023-02-09T02:32:35.236Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:32:29.224Z
---

- [Políticas de red de Kubernetes: aplicación de reglas de comunicación entre pods***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-network-policies-enforcing-communication-rules-between-pods)
{.links-list}
- [Kubernetes 网络策略：在 Pod 之间执行通信规则***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-network-policies-enforcing-communication-rules-between-pods)
{.links-list}
- [Kubernetes 네트워크 정책: Pod 간 통신 규칙 적용***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-network-policies-enforcing-communication-rules-between-pods)
{.links-list}


# Kubernetes Network Policies: Enforcing Communication Rules Between Pods

Kubernetes network policies provide a way to enforce communication rules between pods. By default, all pods in a Kubernetes cluster can communicate with each other. However, in some cases it may be desirable to limit communication to only certain pods. For example, you may want to allow communication between web servers and database servers, but not between web servers and application servers.

Network policies can be used to achieve this by specifying which pods are allowed to communicate with each other. Network policies are implemented as Kubernetes resources, and can be defined using YAML or JSON.

Here is an example network policy that allows communication between web servers and database servers, but not between web servers and application servers:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-db
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - protocol: TCP
      port: 3306
```

This network policy can be applied to a namespace by creating a file named `allow-web-db.yaml` in the `/etc/kubernetes/manifests` directory.

Network policies can also be used to deny communication between certain pods. For example, the following network policy denies all communication between web servers and application servers:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-web-app
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: app
    ports:
    - protocol: TCP
      port: 80
```

This network policy can be applied to a namespace by creating a file named `deny-web-app.yaml` in the `/etc/kubernetes/manifests` directory.

It is also possible to allow communication between certain pods while denying communication between others. For example, the following network policy allows communication between web servers and database servers, but denies communication between web servers and application servers:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-db-deny-web-app
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - protocol: TCP
      port: 3306
  - from:
    - podSelector:
        matchLabels:
          role: app
    ports:
    - protocol: TCP
      port: 80
```

This network policy can be applied to a namespace by creating a file named `allow-web-db-deny-web-app.yaml` in the `/etc/kubernetes/manifests` directory.

Network policies can be very powerful and can be used to implement complex communication rules between pods. However, it is important to note that network policies only work if the pods have been properly label. For more information on how to label pods, see the Kubernetes documentation.

## External Resources

- [Kubernetes Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Labeling Pods](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)