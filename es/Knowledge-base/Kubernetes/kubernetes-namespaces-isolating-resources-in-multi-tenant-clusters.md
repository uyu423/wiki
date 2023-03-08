---
title: Espacios de nombres de Kubernetes: aislamiento de recursos en clústeres de múltiples inquilinos
description: 
published: true
date: 2023-02-08T23:32:19.227Z
tags: 
editor: markdown
dateCreated: 2023-02-08T23:32:17.375Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Namespaces: Isolating Resources in Multi-Tenant Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-namespaces-isolating-resources-in-multi-tenant-clusters)
{.links-list}


# Espacios de nombres de Kubernetes: aislamiento de recursos en clústeres de múltiples inquilinos

Los espacios de nombres de Kubernetes ofrecen una manera simple pero poderosa de aislar recursos en un clúster compartido. Al crear espacios de nombres separados para cada arrendatario, puede controlar qué usuarios tienen acceso a qué recursos y limitar la visibilidad de los recursos entre arrendatarios.

## Creación de espacios de nombres

Puede crear un espacio de nombres ejecutando el comando `kubectl create namespace`. Por ejemplo, para crear un espacio de nombres para un arrendatario llamado `acme`, ejecutaría:

```
kubectl create namespace acme
```

## Asignación de recursos a espacios de nombres

Una vez que se ha creado un espacio de nombres, puede asignarle recursos usando el indicador `--namespace` con el comando `kubectl`. Por ejemplo, para crear un pod en el espacio de nombres `acme`, ejecutaría:

```
kubectl create pod --namespace acme ...
```

## Visualización de recursos en un espacio de nombres

De forma predeterminada, el comando `kubectl` solo mostrará los recursos en el espacio de nombres `predeterminado`. Para ver recursos en un espacio de nombres diferente, puede usar el indicador `--namespace` con el comando `kubectl get`. Por ejemplo, para ver todos los pods en el espacio de nombres `acme`, ejecutaría:

```
kubectl get pods --namespace acme
```

## Cambiar entre espacios de nombres

Si se encuentra ejecutando comandos con frecuencia en un espacio de nombres específico, puede usar el comando `kubectl config set-context` para cambiar entre espacios de nombres. Por ejemplo, para cambiar al espacio de nombres `acme`, ejecutaría:

```
kubectl config set-context $(kubectl config current-context) --namespace=acme
```

## Eliminación de espacios de nombres

Puede eliminar un espacio de nombres ejecutando el comando `kubectl delete namespace`. Por ejemplo, para eliminar el espacio de nombres `acme`, ejecutaría:

```
kubectl delete namespace acme
```

## Conclusión

Los espacios de nombres de Kubernetes ofrecen una manera simple pero poderosa de aislar recursos en un clúster compartido. Al crear espacios de nombres separados para cada arrendatario, puede controlar qué usuarios tienen acceso a qué recursos y limitar la visibilidad de los recursos entre arrendatarios.