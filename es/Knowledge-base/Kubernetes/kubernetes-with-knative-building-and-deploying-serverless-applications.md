---
title: Kubernetes con Knative: creación e implementación de aplicaciones sin servidor
description: 
published: true
date: 2023-02-12T02:17:42.614Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:17:36.017Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with Knative: Building and Deploying Serverless Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-knative-building-and-deploying-serverless-applications)
{.links-list}


# Kubernetes con Knative: creación e implementación de aplicaciones sin servidor

En este artículo, exploraremos cómo usar Kubernetes con Knative para crear e implementar aplicaciones sin servidor. Comenzaremos con una breve descripción general de la computación sin servidor y Kubernetes, seguida de una mirada a cómo encaja Knative en el ecosistema de Kubernetes. Luego, veremos un ejemplo simple de creación e implementación de una aplicación sin servidor con Kubernetes y Knative.

## ¿Qué es la informática sin servidor?

La computación sin servidor es un modelo de ejecución de computación en la nube en el que el proveedor de la nube ejecuta el servidor y el cliente paga solo por el tiempo de computación utilizado. La computación sin servidor es una forma de proporcionar servicios de back-end según sea necesario.

Hay dos tipos de computación sin servidor:

- Función como servicio (FaaS): un servicio que ejecuta el código proporcionado por el usuario bajo demanda.
- Backend como servicio (BaaS): un servicio que proporciona un backend para aplicaciones, como notificaciones push o almacenamiento.

## ¿Qué es Kubernetes?

Kubernetes es una plataforma portátil y extensible de código abierto para administrar cargas de trabajo y servicios en contenedores, que facilita tanto la configuración declarativa como la automatización. Tiene un ecosistema grande y de rápido crecimiento. Los servicios, el soporte y las herramientas de Kubernetes están ampliamente disponibles, incluidas las soluciones alojadas de Kubernetes.

## ¿Qué es Knativo?

Knative es un conjunto de componentes de código abierto que amplían Kubernetes para proporcionar una plataforma para cargas de trabajo sin servidor. Knative consta de tres componentes:

- Servicio: un conjunto de componentes que proporciona una plataforma sin servidor en Kubernetes, incluido un proxy HTTP y recursos informáticos de escalado automático.
- Compilación: un conjunto de componentes que proporciona compilaciones de imágenes de contenedores sin servidor.
- Eventing: un conjunto de componentes que proporciona transmisión y mensajería basada en eventos.

Knative está diseñado para funcionar con cualquier orquestador de contenedores que pueda ejecutar Kubernetes, incluidos Google Kubernetes Engine (GKE), Azure Kubernetes Service (AKS) y Amazon Elastic Container Service for Kubernetes (EKS).

## Creación e implementación de una aplicación sin servidor en Kubernetes

En esta sección, veremos un ejemplo de creación e implementación de una aplicación sin servidor en Kubernetes con Knative. Usaremos un ejemplo simple de "Hola, mundo" escrito en Go.

Primero, crearemos un archivo llamado `main.go` con el siguiente código:

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

A continuación, crearemos un `Dockerfile` con los siguientes contenidos:

```
FROM golang:1.11

WORKDIR /go/src/app

COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["app"]
```

Ahora que tenemos nuestro código y `Dockerfile`, podemos crear nuestra imagen de contenedor y enviarla a un registro de contenedor:

```
$ docker build -t gcr.io/<project-id>/helloworld:v1 .
$ docker push gcr.io/<project-id>/helloworld:v1
```

Reemplace `<project-id>` con su ID de proyecto de Google Cloud Platform.

Una vez que la imagen del contenedor se envía al registro, podemos implementarla en Kubernetes usando el comando `kubectl`:

```
$ kubectl apply -f helloworld.yaml
```

Donde `helloworld.yaml` es un archivo YAML con el siguiente contenido:

```yaml
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: helloworld
  namespace: default
spec:
  template:
    spec:
      containers:
        - image: gcr.io/<project-id>/helloworld:v1
          env:
            - name: TARGET
              value: "World"
```

Una vez que se implementa el servicio, podemos ver la URL de nuestra aplicación:

```
$ kubectl get ksvc
NAME            URL                                                 LATESTCREATED          LATESTREADY             READY     REASON
helloworld      http://helloworld-default.default.svc.cluster.local   helloworld-00001-00000   helloworld-00001-00000   True
```

Y podemos probarlo curvando la URL:

```
$ curl http://helloworld-default.default.svc.cluster.local
Hello, World!
```

## Conclusión

En este artículo, exploramos cómo usar Kubernetes con Knative para crear e implementar aplicaciones sin servidor. Hemos analizado qué es la informática sin servidor y cómo encaja Knative en el ecosistema de Kubernetes. Finalmente, analizamos un ejemplo simple de creación e implementación de una aplicación sin servidor con Kubernetes y Knative.