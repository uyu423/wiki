---
title: API de Kubernetes: interacción con su clúster con solicitudes REST
description: 
published: true
date: 2023-02-14T03:33:32.781Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:33:30.964Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes API: Interacting with Your Cluster with REST Requests***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-api-interacting-with-your-cluster-with-rest-requests)
{.links-list}


# API de Kubernetes: interacción con su clúster con solicitudes REST

En este artículo, veremos cómo usar la API de Kubernetes para interactuar con su clúster de Kubernetes. Cubriremos los conceptos básicos para realizar solicitudes REST a la API de Kubernetes y veremos algunos de los recursos y operaciones de la API más comunes.

## Realización de solicitudes REST

La API de Kubernetes es una API [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer), lo que significa que puede usar cualquier cliente HTTP para realizar solicitudes a la API. Todo lo que necesita hacer es enviar una solicitud HTTP al extremo de la API correspondiente y la API de Kubernetes responderá con los datos solicitados.

Para realizar una solicitud a la API de Kubernetes, debe conocer la URL del extremo de la API al que desea llamar y debe especificar el método HTTP que desea utilizar. Los métodos HTTP más comunes son `GET`, `POST`, `PUT` y `DELETE`.

Por ejemplo, para obtener una lista de todos los pods en un espacio de nombres, haría una solicitud `GET` al extremo `/api/v1/namespaces/{namespace}/pods`. Para crear un nuevo pod, haría una solicitud `POST` al mismo punto final.

Además de la URL y el método HTTP, también debe especificar un [encabezado HTTP] (https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) llamado `Autorización` con un valor de `Bearer {token}`, donde `{token}` es un token de API de Kubernetes válido. Puede obtener un token de la API de Kubernetes ejecutando el comando `kubectl get secrets`.

## Recursos API comunes

Ahora que cubrimos los conceptos básicos para realizar solicitudes REST a la API de Kubernetes, echemos un vistazo a algunos de los recursos de API más comunes.

### vainas

Los pods son las unidades implementables más pequeñas en Kubernetes, y siempre se ubican y programan juntos en el mismo nodo. Un pod representa una única instancia de una aplicación y puede contener uno o más contenedores.

Para obtener una lista de todos los pods en un espacio de nombres, puede realizar una solicitud `GET` al extremo `/api/v1/namespaces/{namespace}/pods`. Para obtener los detalles de un pod específico, puede realizar una solicitud `GET` al extremo `/api/v1/namespaces/{namespace}/pods/{name}`.

Para crear un nuevo pod, puede realizar una solicitud `POST` al extremo `/api/v1/namespaces/{namespace}/pods`. El cuerpo de la solicitud debe ser un objeto [JSON](https://www.json.org/) o [YAML](https://yaml.org/) que especifique la especificación del pod.

Aquí hay un ejemplo de una especificación de pod en JSON:

```json
{
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "nginx-pod",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "nginx",
        "image": "nginx:1.7.9",
        "ports": [
          {
            "containerPort": 80
          }
        ]
      }
    ]
  }
}
```

Y aquí está la misma especificación en YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
```

Para actualizar un pod, puede realizar una solicitud `PUT` o `PATCH` al extremo `/api/v1/namespaces/{namespace}/pods/{name}`. El cuerpo de la solicitud debe ser un objeto JSON o YAML que especifique la especificación del pod.

Para eliminar un pod, puede realizar una solicitud `DELETE` al extremo `/api/v1/namespaces/{namespace}/pods/{name}`.

### Conjuntos de réplicas

Los conjuntos de réplicas son un [recurso de Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) que garantiza que siempre se esté ejecutando una cantidad específica de réplicas de pod. Si un pod se elimina o falla, el conjunto de réplicas se asegurará de que se cree un nuevo pod para reemplazarlo.

Para obtener una lista de todos los conjuntos de réplicas en un espacio de nombres, puede realizar una solicitud `GET` al extremo `/apis/apps/v1/namespaces/{namespace}/replicasets`. Para obtener los detalles de un conjunto de réplicas específico, puede realizar una solicitud `GET` al extremo `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}`.

Para crear un nuevo conjunto de réplicas, puede realizar una solicitud `POST` al extremo `/apis/apps/v1/namespaces/{namespace}/replicasets`. El cuerpo de la solicitud debe ser un objeto JSON o YAML que especifique la especificación del conjunto de réplicas.

Aquí hay un ejemplo de una especificación de conjunto de réplicas en JSON:

```json
{
  "apiVersion": "apps/v1",
  "kind": "ReplicaSet",
  "metadata": {
    "name": "nginx-replicaset",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

Y aquí está la misma especificación en YAML:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

Para actualizar un conjunto de réplicas, puede realizar una solicitud `PUT` o `PATCH` al extremo `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}`. El cuerpo de la solicitud debe ser un objeto JSON o YAML que especifique la especificación del conjunto de réplicas.

Para eliminar un conjunto de réplicas, puede realizar una solicitud `DELETE` al extremo `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}`.

### Despliegues

[Implementaciones](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) son un recurso de nivel superior que administra conjuntos de réplicas y proporciona una forma declarativa de especificar el estado deseado de sus pods. Una implementación define un conjunto de réplicas y garantiza que siempre se esté ejecutando la cantidad especificada de réplicas.

Para obtener una lista de todas las implementaciones en un espacio de nombres, puede realizar una solicitud `GET` al extremo `/apis/apps/v1/namespaces/{namespace}/deployments`. Para obtener los detalles de una implementación específica, puede realizar una solicitud `GET` al extremo `/apis/apps/v1/namespaces/{namespace}/deployments/{name}`.

Para crear una nueva implementación, puede realizar una solicitud `POST` al extremo `/apis/apps/v1/namespaces/{namespace}/deployments`. El cuerpo de la solicitud debe ser un objeto JSON o YAML que especifique la especificación de implementación.

Este es un ejemplo de una especificación de implementación en JSON:

```json
{
  "apiVersion": "apps/v1",
  "kind": "Deployment",
  "metadata": {
    "name": "nginx-deployment",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

Y aquí está la misma especificación en YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

Para actualizar una implementación, puede realizar una solicitud `PUT` o `PATCH` al extremo `/apis/apps/v1/namespaces/{namespace}/deployments/{name}`. El cuerpo de la solicitud debe ser un objeto JSON o YAML que especifique la especificación de implementación.

Para eliminar una implementación, puede realizar una solicitud `DELETE` al extremo `/apis/apps/v1/namespaces/{namespace}/deployments/{name}`.

## Conclusión

En este artículo, cubrimos los aspectos básicos de la interacción con la API de Kubernetes mediante solicitudes REST. Hemos analizado algunos de los recursos de API más comunes y hemos visto cómo usar la API de Kubernetes para crear, leer, actualizar y eliminar esos recursos.