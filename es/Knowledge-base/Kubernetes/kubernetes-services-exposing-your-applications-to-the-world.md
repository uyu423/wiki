---
title: Servicios de Kubernetes: exposición de sus aplicaciones al mundo
description: 
published: true
date: 2023-02-06T08:55:28.038Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:55:26.486Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Services: Exposing Your Applications to the World***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}


# Servicios de Kubernetes: exponiendo sus aplicaciones al mundo

En una implementación tradicional, cuando desea exponer un nuevo servicio al mundo, debe actualizar las reglas de su firewall para permitir que el tráfico llegue a su nuevo servicio. En una implementación en contenedores que usa Kubernetes, puede usar un objeto "Servicio" para exponer sus aplicaciones al mundo.

Un Servicio en Kubernetes es una abstracción que define un conjunto lógico de Pods y una política mediante la cual acceder a ellos, a veces denominado microservicio. A cada Servicio se le asigna una dirección IP única (a veces denominada "IP de clúster"), que utilizan los servidores proxy del Servicio (consulte a continuación) y forma parte de cualquier URL utilizada para acceder al Servicio.

Hay dos tipos de Servicios en Kubernetes: `ClusterIP` y `NodePort`.

Los servicios `ClusterIP`, el tipo de servicio predeterminado de Kubernetes, exponen el servicio en una IP interna en el clúster. Este tipo hace que el servicio solo sea accesible desde dentro del clúster.

Los servicios `NodePort` exponen el servicio en el mismo puerto de cada nodo en el clúster. Este tipo hace que se pueda acceder al Servicio desde fuera del clúster en la IP de cada Nodo en un puerto estático (el `NodePort`). Puede usar los servicios `NodePort` para exponer una aplicación que se ejecuta en un clúster de Kubernetes en Internet.

En este artículo, nos centraremos en los servicios `NodePort`.

## Creación de un servicio

Digamos que tenemos una implementación con dos Pods, cada uno ejecutando un servidor web simple en el puerto 8080. Podemos exponer estos Pods al mundo con un servicio `NodePort` como este:

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

En este ejemplo, hemos definido un servicio llamado `my-service` que selecciona Pods con la etiqueta `app` establecida en `my-app`. También hemos definido que el Servicio debe exponer el puerto 80 (el `puerto`) y reenviar el tráfico al puerto 8080 en los Pods seleccionados (el `targetPort`).

## Acceso al Servicio

Una vez que haya creado un servicio, puede acceder a él desde fuera del clúster en la IP de cada nodo en `NodePort`:

```
http://<Node IP>:<NodePort>
```

Por ejemplo, si tenemos un Servicio con un `NodePort` de 31001, podemos acceder a él en:

```
http://<Node IP>:31001
```

## Conclusión

En este artículo, hemos visto cómo usar los servicios `NodePort` para exponer aplicaciones que se ejecutan en un clúster de Kubernetes en Internet. Hemos visto cómo crear un Servicio y cómo acceder a él desde fuera del clúster.