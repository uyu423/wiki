---
title: Kubernetes con CSI: administración de almacenamiento para sus clústeres
description: 
published: true
date: 2023-02-14T12:32:40.244Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:32:38.592Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with CSI: Managing Storage for Your Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-csi-managing-storage-for-your-clusters)
{.links-list}


# Kubernetes con CSI: administración de almacenamiento para sus clústeres

La interfaz de almacenamiento de contenedores (CSI) es un conjunto de API que utilizan las soluciones de orquestación de contenedores, como Kubernetes, para aprovisionar y administrar el almacenamiento en bloque para sus aplicaciones. Si bien Kubernetes tiene soporte integrado para algunas soluciones de almacenamiento, como Google Cloud Storage, el uso de CSI le permite a Kubernetes admitir una gama más amplia de soluciones de almacenamiento.

En este artículo, veremos cómo usar CSI con Kubernetes para administrar el almacenamiento de sus clústeres. También conoceremos algunos de los beneficios de usar CSI y cómo puede ayudarlo a administrar más fácilmente el almacenamiento para sus aplicaciones.

## ¿Qué es CSI?

La interfaz de almacenamiento de contenedores (CSI) es un conjunto de API que utilizan las soluciones de orquestación de contenedores, como Kubernetes, para aprovisionar y administrar el almacenamiento en bloque para sus aplicaciones. Si bien Kubernetes tiene soporte integrado para algunas soluciones de almacenamiento, como Google Cloud Storage, el uso de CSI le permite a Kubernetes admitir una gama más amplia de soluciones de almacenamiento.

CSI proporciona un conjunto de API que se pueden usar para aprovisionar y administrar el almacenamiento de contenedores. Por ejemplo, puede usar CSI para crear un volumen de almacenamiento para un contenedor, adjuntarlo a un contenedor en ejecución o desconectarlo de un contenedor en ejecución. También puede usar CSI para tomar una instantánea del volumen de almacenamiento de un contenedor o eliminar un volumen de almacenamiento.

## Cómo usar CSI con Kubernetes

Usar CSI con Kubernetes es simple. Primero, deberá instalar el controlador CSI para su solución de almacenamiento en cada uno de sus nodos de Kubernetes. A continuación, deberá crear una clase de almacenamiento para su solución de almacenamiento. Finalmente, deberá crear una reclamación de volumen persistente (PVC) para cada una de sus aplicaciones que requieran almacenamiento.

La instalación del controlador CSI está fuera del alcance de este artículo, pero puede encontrar instrucciones para hacerlo en la documentación de su solución de almacenamiento.

Una vez que haya instalado el controlador CSI, puede crear una clase de almacenamiento para su solución de almacenamiento. Una clase de almacenamiento define las características del almacenamiento que se utilizará para sus aplicaciones. Por ejemplo, una clase de almacenamiento puede definir el tamaño del almacenamiento, el factor de replicación y el perfil de rendimiento.

Para crear una clase de almacenamiento, deberá usar la herramienta de línea de comandos kubectl. El siguiente comando creará una clase de almacenamiento para una solución de almacenamiento hipotética llamada "mystorage":

```
kubectl create storage-class mystorage \
--provisioner=csi.mystorage.com \
--parameters=size=1Gi,replicationFactor=3,performanceProfile=low
```

Una vez que haya definido una clase de almacenamiento, puede crear un PVC para cada una de sus aplicaciones que requieran almacenamiento. Una PVC es una solicitud de almacenamiento de una clase de almacenamiento en particular. Por ejemplo, el siguiente PVC solicita un gigabyte de almacenamiento de la clase de almacenamiento "mystorage":

```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mystorage-pvc
  namespace: default
spec:
  storageClassName: mystorage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

Cuando crea una PVC, Kubernetes aprovisionará un volumen de almacenamiento de la clase de almacenamiento y lo vinculará a la PVC. A continuación, puede utilizar el PVC para montar el volumen de almacenamiento en un contenedor.

## Beneficios de usar CSI

Hay una serie de beneficios al usar CSI con Kubernetes:

- **Administración de almacenamiento simplificada**: el uso de CSI con Kubernetes puede ayudar a simplificar la administración de almacenamiento para sus aplicaciones. Por ejemplo, puede utilizar una única clase de almacenamiento para aprovisionar almacenamiento para varias aplicaciones.

- **Mayor flexibilidad de la solución de almacenamiento**: CSI permite que Kubernetes admita una gama más amplia de soluciones de almacenamiento. Esto puede resultar útil si utiliza una solución de almacenamiento que Kubernetes no admite de forma nativa.

- **Integración mejorada de la solución de almacenamiento**: CSI puede ayudar a mejorar la integración entre Kubernetes y las soluciones de almacenamiento. Por ejemplo, algunas soluciones de almacenamiento pueden proporcionar funciones adicionales, como instantáneas y replicación, que se pueden usar con Kubernetes.

## Conclusión

En este artículo, analizamos cómo usar CSI con Kubernetes para administrar el almacenamiento de sus aplicaciones. También aprendimos sobre algunos de los beneficios de usar CSI, como la administración de almacenamiento simplificada y una mayor flexibilidad de la solución de almacenamiento.