---
title: 075: Implementación de aplicaciones TensorFlow.js en Kubernetes con Node.js
description: 
published: true
date: 2023-02-03T00:17:49.268Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:17:44.589Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [075: Deploying TensorFlow.js Applications on Kubernetes with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/075-deploying-tensorflow-js-applications-on-kubernetes-with-node-js)
{.links-list}


# 075: Implementación de aplicaciones TensorFlow.js en Kubernetes con Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript, y Node.js es un tiempo de ejecución popular para aplicaciones de JavaScript del lado del servidor. En esta publicación, le mostraremos cómo implementar una aplicación TensorFlow.js en Kubernetes, una popular plataforma de orquestación de contenedores.

Kubernetes es una excelente plataforma para implementar aplicaciones en contenedores a escala. Proporciona características como escalado automático, equilibrio de carga y actualizaciones continuas, que pueden ser de gran ayuda al administrar una aplicación grande.

Node.js es un tiempo de ejecución popular para aplicaciones JavaScript del lado del servidor. Es rápido y tiene un gran ecosistema de bibliotecas y herramientas.

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. Le permite entrenar e implementar modelos en el navegador o en Node.js.

La implementación de una aplicación TensorFlow.js en Kubernetes puede ser una excelente manera de mejorar la disponibilidad y el rendimiento de su aplicación. Kubernetes puede proporcionar funciones como el escalado automático y el equilibrio de carga, que pueden ser de gran ayuda al administrar una aplicación grande.

En esta publicación, le mostraremos cómo implementar una aplicación TensorFlow.js en Kubernetes. Asumiremos que tiene conocimientos básicos de Kubernetes y TensorFlow.js. Si es nuevo en Kubernetes, puede consultar nuestra publicación Kubernetes 101.

## Requisitos previos

Antes de comenzar, deberá tener lo siguiente:

- Un clúster de Kubernetes. Si no tiene uno, puede consultar nuestra guía sobre cómo crear un clúster de Kubernetes.
- Una aplicación TensorFlow.js. Si no tiene uno, puede consultar nuestra guía sobre cómo crear una aplicación TensorFlow.js.

## Implementación de la aplicación

Una vez que tenga un clúster de Kubernetes y una aplicación TensorFlow.js, puede implementar la aplicación en Kubernetes.

Asumiremos que tiene conocimientos básicos de Kubernetes y TensorFlow.js. Si es nuevo en Kubernetes, puede consultar nuestra publicación Kubernetes 101.

Para implementar la aplicación, deberá crear una implementación de Kubernetes. Una implementación es un objeto de Kubernetes que describe un estado deseado para un grupo de pods.

Para crear una implementación, deberá crear un archivo YAML que describa la implementación. Aquí hay un archivo YAML de ejemplo que describe una implementación para una aplicación TensorFlow.js:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tfjs-deployment
spec:
  selector:
    matchLabels:
      app: tfjs-app
  replicas: 1
  template:
    metadata:
      labels:
        app: tfjs-app
    spec:
      containers:
      - name: tfjs-container
        image: <your-docker-image>
        ports:
        - containerPort: 3000
```

En el archivo YAML, deberá especificar la imagen para el contenedor. Esta debería ser la imagen de su aplicación TensorFlow.js.

Una vez que tenga el archivo YAML, puede crear la implementación ejecutando el siguiente comando:

```
kubectl apply -f <your-yaml-file>
```

Esto creará una implementación en su clúster de Kubernetes. La implementación creará un pod que ejecuta su aplicación TensorFlow.js.

## Acceso a la aplicación

Una vez creada la implementación, puede acceder a la aplicación creando un servicio. Un servicio es un objeto de Kubernetes que proporciona una forma de acceder a un grupo de pods.

Para crear un Servicio, deberá crear un archivo YAML que describa el Servicio. Este es un archivo YAML de ejemplo que describe un servicio para una aplicación TensorFlow.js:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: tfjs-service
spec:
  type: LoadBalancer
  selector:
    app: tfjs-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
```

En el archivo YAML, deberá especificar el selector para el Servicio. Esto debería coincidir con el selector de etiquetas para la implementación.

Una vez que tenga el archivo YAML, puede crear el Servicio ejecutando el siguiente comando:

```
kubectl apply -f <your-yaml-file>
```

Esto creará un servicio en su clúster de Kubernetes. El Servicio proporcionará una forma de acceder al pod que ejecuta su aplicación TensorFlow.js.

## Eliminar la implementación

Una vez que haya terminado con la implementación, puede eliminarla ejecutando el siguiente comando:

```
kubectl delete deployment tfjs-deployment
```

Esto eliminará la implementación y el pod que creó.