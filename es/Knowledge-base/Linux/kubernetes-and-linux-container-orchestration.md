---
title: Orquestación de contenedores de Kubernetes y Linux
description: 
published: true
date: 2023-02-12T03:32:21.441Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:32:14.469Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes and Linux Container Orchestration***English** document is available*](/en/Knowledge-base/Linux/kubernetes-and-linux-container-orchestration)
{.links-list}


# ¿Qué es Kubernetes?

Kubernetes es una plataforma de orquestación de contenedores de código abierto diseñada originalmente por Google. Ahora es mantenido por Cloud Native Computing Foundation. Se puede utilizar para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores.

# ¿Qué es un contenedor de Linux?

Un contenedor de Linux es un paquete de software que contiene todos los componentes necesarios para ejecutar una aplicación o servicio en un entorno aislado. Los contenedores son una alternativa a las máquinas virtuales y pueden proporcionar muchos beneficios, como una mejor utilización de recursos, portabilidad y seguridad.

# Orquestación de contenedores de Kubernetes y Linux

Kubernetes se usa a menudo para la orquestación de contenedores, que es la gestión de múltiples contenedores. Esto puede incluir tareas como implementar, escalar y monitorear contenedores. Los contenedores de Linux se pueden usar con Kubernetes para proporcionar un entorno de aplicación ligero y portátil.

# Primeros pasos con Kubernetes

Hay algunas opciones de instalación de Kubernetes, incluido el uso de una solución alojada o la instalación en su propia infraestructura. Para fines de desarrollo y prueba, también puede usar un clúster de Kubernetes de un solo nodo, que se puede ejecutar en una plataforma de contenedores de Linux como Docker.

Una vez que haya instalado Kubernetes, puede comenzar a implementar aplicaciones. Para hacer esto, deberá crear un archivo de implementación de Kubernetes. Este archivo contiene toda la información necesaria sobre su aplicación, como la imagen del contenedor que se usará, la cantidad de réplicas y los puertos expuestos.

Aquí hay un archivo de implementación de ejemplo para una aplicación PHP simple:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-php-app
  labels:
    app: my-php-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-php-app
  template:
    metadata:
      labels:
        app: my-php-app
    spec:
      containers:
      - name: my-php-app
        image: php:7.2-apache
        ports:
        - containerPort: 80
```

Este archivo se puede usar para implementar la aplicación ejecutando el siguiente comando:

```
$ kubectl apply -f my-php-app.yaml
```

# Conclusión

Kubernetes es una poderosa herramienta para administrar aplicaciones en contenedores. Se puede utilizar para automatizar la implementación, el escalado y la gestión de contenedores. Los contenedores de Linux se pueden usar con Kubernetes para proporcionar un entorno de aplicación ligero y portátil.