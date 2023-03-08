---
title: 044: Uso de Nest.js con Kubernetes
description: 
published: true
date: 2023-02-15T16:33:14.942Z
tags: 
editor: markdown
dateCreated: 2023-02-15T16:33:13.078Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [044: Using Nest.js with Kubernetes***English** document is available*](/en/Knowledge-base/Nest-js/Learning/044-using-nest-js-with-kubernetes)
{.links-list}


# Uso de Nest.js con Kubernetes

Kubernetes es una poderosa herramienta de orquestación de contenedores y Nest.js es un marco popular de Node.js. En esta publicación, le mostraremos cómo usar Nest.js con Kubernetes.

## Requisitos previos

- Un clúster de Kubernetes
- Un editor de texto

## Instalación de Nest.js

Primero, necesitamos instalar Nest.js. Podemos hacer esto usando el administrador de paquetes de Node.js, npm:

```
npm install -g @nestjs/cli
```

## Creación de un proyecto Nest.js

Una vez que se instala Nest.js, podemos crear un nuevo proyecto usando la CLI de Nest.js:

```
nest new project-name
```

## Ejecutar un proyecto Nest.js

Podemos ejecutar nuestro proyecto Nest.js usando el siguiente comando:

```
npm run start
```

## Implementación de un proyecto Nest.js en Kubernetes

Podemos implementar nuestro proyecto Nest.js en Kubernetes usando la herramienta de línea de comandos kubectl.

Primero, necesitamos crear un archivo llamado `nest-deployment.yaml` con los siguientes contenidos:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nest-deployment
spec:
  selector:
    matchLabels:
      app: nest
  replicas: 2
  template:
    metadata:
      labels:
        app: nest
    spec:
      containers:
      - name: nest
        image: YOUR_DOCKER_HUB_USERNAME/nest
        ports:
        - containerPort: 8080
```

Reemplace `YOUR_DOCKER_HUB_USERNAME` con su nombre de usuario de Docker Hub.

A continuación, debemos compilar nuestro proyecto Nest.js y enviarlo a Docker Hub:

```
docker build -t YOUR_DOCKER_HUB_USERNAME/nest .
docker push YOUR_DOCKER_HUB_USERNAME/nest
```

Finalmente, podemos implementar nuestro proyecto Nest.js en Kubernetes:

```
kubectl apply -f nest-deployment.yaml
```

## Acceso a una aplicación Nest.js

Podemos acceder a nuestra aplicación Nest.js a través de la dirección IP del clúster de Kubernetes:

```
http://CLUSTER_IP:8080
```

Reemplace `CLUSTER_IP` con la dirección IP de su clúster de Kubernetes.

## Conclusión

En esta publicación, le mostramos cómo usar Nest.js con Kubernetes. Instalamos Nest.js, creamos un nuevo proyecto y lo implementamos en Kubernetes. También le mostramos cómo acceder a su aplicación Nest.js a través de la dirección IP del clúster de Kubernetes.