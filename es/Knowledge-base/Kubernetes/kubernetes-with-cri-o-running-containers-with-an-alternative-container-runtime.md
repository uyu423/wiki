---
title: Kubernetes con CRI-O: ejecución de contenedores con un tiempo de ejecución de contenedor alternativo
description: 
published: true
date: 2023-02-14T09:32:29.308Z
tags: 
editor: markdown
dateCreated: 2023-02-14T09:32:22.073Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with CRI-O: Running Containers with an Alternative Container Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-cri-o-running-containers-with-an-alternative-container-runtime)
{.links-list}


# Kubernetes con CRI-O: ejecución de contenedores con un tiempo de ejecución de contenedor alternativo

## ¿Qué es CRI-O?

CRI-O es un tiempo de ejecución de contenedor alternativo para Kubernetes. Está diseñado para ser liviano y ocupar un espacio mínimo, lo que lo hace ideal para ejecutar contenedores en Kubernetes. CRI-O utiliza la especificación de tiempo de ejecución de Open Containers Initiative (OCI) y es compatible con Kubernetes CRI (Container Runtime Interface).

## ¿Por qué usar CRI-O con Kubernetes?

Hay algunas razones por las que podría querer usar CRI-O con Kubernetes:

- CRI-O está diseñado para ser liviano y ocupar un espacio mínimo. Esto lo hace ideal para ejecutar contenedores en Kubernetes.
- CRI-O utiliza la especificación de tiempo de ejecución de Open Containers Initiative (OCI). Esto significa que es compatible con Kubernetes CRI (Container Runtime Interface).
- CRI-O está integrado con el complemento de interfaz de red de contenedores (CNI) de Kubernetes. Esto facilita la configuración de redes para contenedores que se ejecutan en Kubernetes.

## Cómo usar CRI-O con Kubernetes

Usar CRI-O con Kubernetes es fácil. Puede usar el tiempo de ejecución del contenedor CRI-O directamente o usar la integración CRI-O Kubernetes.

### Usando el tiempo de ejecución del contenedor CRI-O directamente

Para usar el tiempo de ejecución del contenedor CRI-O directamente, debe configurar el indicador `--runtime` al iniciar el `kubelet` de Kubernetes:

```
$ kubelet --runtime=cri-o
```

### Uso de la integración CRI-O Kubernetes

Para utilizar la integración CRI-O Kubernetes, debe configurar el indicador `--container-runtime` al iniciar el `kubelet` de Kubernetes:

```
$ kubelet --container-runtime=cri-o
```

También debe configurar el indicador `--feature-gates` para habilitar la integración de CRI-O Kubernetes:

```
$ kubelet --feature-gates=CRIO=true
```

## Conclusión

CRI-O es un gran tiempo de ejecución de contenedor alternativo para Kubernetes. Está diseñado para ser liviano y ocupar un espacio mínimo, lo que lo hace ideal para ejecutar contenedores en Kubernetes. CRI-O utiliza la especificación de tiempo de ejecución de Open Containers Initiative (OCI) y es compatible con Kubernetes CRI (Container Runtime Interface). CRI-O también está integrado con el complemento de interfaz de red de contenedores (CNI) de Kubernetes. Esto facilita la configuración de redes para contenedores que se ejecutan en Kubernetes.