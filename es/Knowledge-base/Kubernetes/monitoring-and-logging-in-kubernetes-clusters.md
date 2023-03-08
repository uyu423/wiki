---
title: Supervisión y registro en clústeres de Kubernetes
description: 
published: true
date: 2023-02-08T19:32:28.322Z
tags: 
editor: markdown
dateCreated: 2023-02-08T19:32:22.530Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Monitoring and Logging in Kubernetes Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/monitoring-and-logging-in-kubernetes-clusters)
{.links-list}


# Monitoreo y registro en clústeres de Kubernetes

En este artículo, exploraremos cómo monitorear y registrar la actividad en los clústeres de Kubernetes. Comenzaremos con una descripción general de los tipos de datos que normalmente se recopilan para monitorear y registrar, y luego nos sumergiremos en algunas herramientas y técnicas específicas que se pueden usar para recopilar estos datos.

## Tipos de datos recopilados para monitoreo y registro

Hay dos tipos principales de datos que se recopilan para monitorear y registrar: datos del sistema y datos de la aplicación.

Los datos del sistema incluyen información sobre los nodos en el clúster de Kubernetes, como el uso de CPU y memoria, el tráfico de red y la actividad del disco. Estos datos generalmente se recopilan utilizando una herramienta como Prometheus.

Los datos de la aplicación incluyen información sobre las aplicaciones que se ejecutan en el clúster de Kubernetes, como los tiempos de solicitud y respuesta, las tasas de error y las solicitudes más lentas. Estos datos generalmente se recopilan utilizando una herramienta como Fluentd.

## Recopilación de datos del sistema

Prometheus es una popular herramienta de código abierto para recopilar datos del sistema. Prometheus se puede usar para recopilar datos de cualquier tipo de sistema, pero tiene un soporte especialmente bueno para Kubernetes.

Prometheus recopila datos extrayendo métricas de puntos finales HTTP. De forma predeterminada, Kubernetes expone una serie de métricas en el formato Prometheus en el extremo `/metrics`. Prometheus puede extraer estas métricas para proporcionar información valiosa sobre el estado y el rendimiento del clúster de Kubernetes.

Además de las métricas integradas, Kubernetes también expone un punto final `/logs` que Prometheus puede raspar para recopilar datos de registro. Estos datos se pueden utilizar para generar alertas o para visualizar el estado de las aplicaciones que se ejecutan en el clúster.

## Recopilación de datos de la aplicación

Fluentd es una popular herramienta de código abierto para recopilar datos de aplicaciones. Fluentd se puede usar para recopilar datos de cualquier tipo de aplicación, pero tiene un soporte especialmente bueno para Kubernetes.

Fluentd recopila datos mediante el análisis de archivos de registro. De forma predeterminada, Kubernetes escribe todos los datos de registro en archivos en el directorio `/var/log/containers`. Fluentd se puede configurar para observar este directorio y analizar los datos de registro para extraer información útil, como los tiempos de solicitud y respuesta, las tasas de error y las solicitudes más lentas.

Estos datos pueden luego almacenarse en una base de datos para su posterior análisis o usarse para generar alertas. Fluentd también admite una amplia variedad de formatos de salida, por lo que los datos se pueden integrar fácilmente con otras herramientas y sistemas.

## Conclusión

En este artículo, exploramos cómo recopilar datos de aplicaciones y sistemas para monitorear e iniciar sesión en Kubernetes. Hemos visto cómo se puede usar Prometheus para recopilar datos del sistema y cómo se puede usar Fluentd para recopilar datos de aplicaciones.

Ambas herramientas son altamente configurables y admiten una amplia variedad de formatos de entrada y salida. Esto los hace fáciles de integrar con otras herramientas y sistemas.

## Referencias

1. Prometeo: https://prometheus.io/
2. Fluentd: https://www.fluentd.org/
3. Supervisión de Kubernetes: https://kubernetes.io/docs/concepts/cluster-administration/monitoring/