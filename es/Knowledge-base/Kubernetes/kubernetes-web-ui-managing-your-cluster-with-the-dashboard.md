---
title: Interfaz de usuario web de Kubernetes: administración de su clúster con el tablero
description: 
published: true
date: 2023-02-14T02:32:33.112Z
tags: 
editor: markdown
dateCreated: 2023-02-14T02:32:25.897Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Web UI: Managing Your Cluster with the Dashboard***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-web-ui-managing-your-cluster-with-the-dashboard)
{.links-list}


# Interfaz de usuario web de Kubernetes: administración de su clúster con el tablero

Kubernetes es una poderosa herramienta de orquestación de contenedores que puede ayudarlo a administrar sus aplicaciones y recursos a escala. El panel de Kubernetes es una interfaz de usuario basada en la web que puede ayudarlo a administrar su clúster de Kubernetes. En este artículo, veremos cómo usar el panel para administrar su clúster.

## Accediendo al Tablero

Para acceder al panel, deberá tener un clúster de Kubernetes en funcionamiento. Puede seguir las instrucciones de la documentación de Kubernetes para [configurar un clúster local](https://kubernetes.io/docs/setup/learning-environment/minikube/).

Una vez que tenga un clúster en funcionamiento, puede acceder al panel ejecutando el siguiente comando:

```
kubectl proxy
```

Esto iniciará un proxy para el servidor API de Kubernetes y hará que el panel esté disponible en http://localhost:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard:/proxy/.

## Creación de un clúster de Kubernetes

Para crear un clúster de Kubernetes, deberá tener un clúster de Kubernetes en ejecución. Puede seguir las instrucciones de la documentación de Kubernetes para [configurar un clúster local](https://kubernetes.io/docs/setup/learning-environment/minikube/).

Una vez que tenga un clúster de Kubernetes en funcionamiento, puede crear un nuevo clúster ejecutando el siguiente comando:

```
kubectl create cluster my-cluster
```

Puede verificar que el clúster se creó ejecutando el siguiente comando:

```
kubectl get clusters
```

## Eliminación de un clúster de Kubernetes

Para eliminar un clúster de Kubernetes, deberá tener un clúster de Kubernetes en ejecución. Puede seguir las instrucciones de la documentación de Kubernetes para [configurar un clúster local](https://kubernetes.io/docs/setup/learning-environment/minikube/).

Una vez que tenga un clúster de Kubernetes en funcionamiento, puede eliminar un clúster ejecutando el siguiente comando:

```
kubectl delete cluster my-cluster
```

Puede verificar que el clúster se eliminó ejecutando el siguiente comando:

```
kubectl get clusters
```

## Gestión de nodos

El panel de Kubernetes se puede usar para administrar nodos en un clúster de Kubernetes. Para ver una lista de nodos en el clúster, haga clic en el enlace "Nodos" en la barra de navegación de la izquierda. Esto abrirá una página que enumera todos los nodos en el clúster.

Desde esta página, puede ver información sobre cada nodo, como su dirección IP, sistema operativo y versión del kernel. También puede realizar acciones en los nodos, como eliminarlos o escalarlos hacia arriba o hacia abajo.

## Gestión de pods

El panel de Kubernetes se puede usar para administrar pods en un clúster de Kubernetes. Para ver una lista de pods en el clúster, haga clic en el enlace "Pods" en la barra de navegación de la izquierda. Esto abrirá una página que enumera todos los pods en el clúster.

Desde esta página, puede ver información sobre cada pod, como su dirección IP y los nodos en los que se ejecuta. También puede realizar acciones en los pods, como eliminarlos o aumentarlos o reducirlos.

## Gestión de implementaciones

El panel de Kubernetes se puede usar para administrar implementaciones en un clúster de Kubernetes. Para ver una lista de implementaciones en el clúster, haga clic en el enlace "Implementaciones" en la barra de navegación de la izquierda. Esto abrirá una página que enumera todas las implementaciones en el clúster.

Desde esta página, puede ver información sobre cada implementación, como la cantidad de réplicas y los pods que forman parte de la implementación. También puede realizar acciones en implementaciones, como escalarlas hacia arriba o hacia abajo.

## Gestión de servicios

El panel de Kubernetes se puede usar para administrar servicios en un clúster de Kubernetes. Para ver una lista de servicios en el clúster, haga clic en el enlace "Servicios" en la barra de navegación de la izquierda. Esto abrirá una página que enumera todos los servicios en el clúster.

Desde esta página, puede ver información sobre cada servicio, como el tipo de servicio y los pods que forman parte del servicio. También puede realizar acciones en los servicios, como editar el servicio o eliminarlo.

## Conclusión

En este artículo, hemos visto cómo usar el Panel de control de Kubernetes para administrar un clúster de Kubernetes. Hemos analizado cómo crear y eliminar clústeres, cómo administrar nodos y pods, y cómo administrar implementaciones y servicios.