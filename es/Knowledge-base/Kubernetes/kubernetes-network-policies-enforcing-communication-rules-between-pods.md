---
title: Políticas de red de Kubernetes: aplicación de reglas de comunicación entre pods
description: 
published: true
date: 2023-02-09T02:32:30.800Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:32:29.223Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Network Policies: Enforcing Communication Rules Between Pods***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-network-policies-enforcing-communication-rules-between-pods)
{.links-list}


# Políticas de red de Kubernetes: aplicación de reglas de comunicación entre pods

Las políticas de red de Kubernetes proporcionan una forma de hacer cumplir las reglas de comunicación entre los pods. De forma predeterminada, todos los pods en un clúster de Kubernetes pueden comunicarse entre sí. Sin embargo, en algunos casos puede ser conveniente limitar la comunicación solo a ciertos pods. Por ejemplo, es posible que desee permitir la comunicación entre servidores web y servidores de bases de datos, pero no entre servidores web y servidores de aplicaciones.

Las políticas de red se pueden usar para lograr esto especificando qué pods pueden comunicarse entre sí. Las políticas de red se implementan como recursos de Kubernetes y se pueden definir mediante YAML o JSON.

Aquí hay una política de red de ejemplo que permite la comunicación entre servidores web y servidores de bases de datos, pero no entre servidores web y servidores de aplicaciones:

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

Esta política de red se puede aplicar a un espacio de nombres creando un archivo llamado `allow-web-db.yaml` en el directorio `/etc/kubernetes/manifests`.

Las políticas de red también se pueden usar para denegar la comunicación entre ciertos pods. Por ejemplo, la siguiente política de red niega toda comunicación entre servidores web y servidores de aplicaciones:

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

Esta política de red se puede aplicar a un espacio de nombres creando un archivo llamado `deny-web-app.yaml` en el directorio `/etc/kubernetes/manifests`.

También es posible permitir la comunicación entre ciertos pods y negar la comunicación entre otros. Por ejemplo, la siguiente política de red permite la comunicación entre servidores web y servidores de bases de datos, pero niega la comunicación entre servidores web y servidores de aplicaciones:

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

Esta política de red se puede aplicar a un espacio de nombres creando un archivo llamado `allow-web-db-deny-web-app.yaml` en el directorio `/etc/kubernetes/manifests`.

Las políticas de red pueden ser muy poderosas y se pueden usar para implementar reglas de comunicación complejas entre pods. Sin embargo, es importante tener en cuenta que las políticas de red solo funcionan si los pods se han etiquetado correctamente. Para obtener más información sobre cómo etiquetar pods, consulte la documentación de Kubernetes.

## Recursos externos

- [Políticas de red de Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Cápsulas de etiquetado](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)