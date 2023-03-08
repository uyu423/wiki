---
title: Redes de Kubernetes: comunicación entre pods y servicios
description: 
published: true
date: 2023-02-08T20:32:16.168Z
tags: 
editor: markdown
dateCreated: 2023-02-08T20:32:14.555Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Networking: Communication Between Pods and Services***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-networking-communication-between-pods-and-services)
{.links-list}


# Redes de Kubernetes: comunicación entre pods y servicios

La red de Kubernetes es un tema complejo, aún más por el hecho de que hay varias formas diferentes de configurarlo. En este artículo, nos centraremos en la comunicación entre los pods y los servicios.

Los pods son las unidades básicas de implementación en Kubernetes y se pueden considerar como contenedores con esteroides. Pueden contener múltiples contenedores, tener su propia dirección IP y pueden usarse para aislar aplicaciones entre sí.

Los servicios se utilizan para exponer aplicaciones que se ejecutan en pods al mundo exterior. Se pueden exponer utilizando varios métodos diferentes, incluidos ClusterIP, NodePort y LoadBalancer.

Cuando se crea un servicio, Kubernetes crea una dirección IP virtual (VIP) que se usa para enrutar el tráfico a los pods que forman parte de ese servicio.

## Comunicación entre pods

La capa de red de Kubernetes maneja la comunicación entre los pods. De forma predeterminada, a cada pod se le asigna una dirección IP única dentro del clúster y puede comunicarse con otros pods mediante esta dirección.

Los pods también pueden comunicarse entre sí mediante nombres de host. De forma predeterminada, a cada pod se le asigna un nombre de host que se basa en su dirección IP. Por ejemplo, si un pod tiene una dirección IP de 10.0.0.1, su nombre de host sería 1-10-0-0-1.pods.cluster.local.

## Comunicación entre servicios

La capa de red de Kubernetes maneja la comunicación entre los servicios. De forma predeterminada, a cada servicio se le asigna una dirección IP única dentro del clúster y puede comunicarse con otros servicios utilizando esta dirección.

Los servicios también pueden comunicarse entre sí mediante nombres de host. De forma predeterminada, a cada servicio se le asigna un nombre de host que se basa en su dirección IP. Por ejemplo, si un servicio tiene una dirección IP de 10.0.0.1, su nombre de host sería 1-10-0-0-1.services.cluster.local.

## Comunicación entre pods y servicios

Los pods pueden comunicarse con los servicios utilizando la dirección IP o el nombre de host del servicio. De forma predeterminada, a los pods se les asigna un nombre de host que se basa en la dirección IP del servicio. Por ejemplo, si un pod tiene una dirección IP de 10.0.0.1 y un servicio tiene una dirección IP de 10.0.0.2, el pod podría comunicarse con el servicio utilizando el nombre de host 2-10-0-0-2.services .cluster.local.

Los pods también pueden comunicarse con los servicios mediante la dirección ClusterIP del servicio. De forma predeterminada, la dirección ClusterIP se asigna a la interfaz de red predeterminada del pod. Por ejemplo, si un pod tiene una dirección IP de 10.0.0.1 y un servicio tiene una dirección ClusterIP de 10.0.0.2, el pod podría comunicarse con el servicio mediante la dirección ClusterIP.

## Conclusión

Las redes de Kubernetes son un tema complejo, pero la comunicación entre los pods y los servicios es una parte clave. En este artículo, cubrimos los conceptos básicos de cómo los pods y los servicios se comunican entre sí.