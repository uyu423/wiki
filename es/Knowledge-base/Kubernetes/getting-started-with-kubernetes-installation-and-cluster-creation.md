---
title: Introducción a Kubernetes: instalación y creación de clústeres
description: 
published: true
date: 2023-02-08T17:33:01.911Z
tags: 
editor: markdown
dateCreated: 2023-02-08T17:32:52.671Z
---

---
title: Introducción a Kubernetes: instalación y creación de clústeres
description: 
published: true
date: 2023-02-08T17:32:52.671Z
tags: 
editor: markdown
dateCreated: 2023-02-08T17:32:52.671Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Getting Started with Kubernetes: Installation and Cluster Creation***English** document is available*](/en/Knowledge-base/Kubernetes/getting-started-with-kubernetes-installation-and-cluster-creation)
{.links-list}


# Introducción a Kubernetes: instalación y creación de clústeres

Kubernetes es una poderosa herramienta de orquestación de contenedores que puede ayudarlo a automatizar la implementación, el escalado y la administración de sus aplicaciones en contenedores. En este artículo, le mostraremos cómo instalar Kubernetes en su máquina local y crear un clúster de Kubernetes.

## Requisitos previos

Antes de comenzar, necesitará lo siguiente:

- Una máquina local con Linux o Windows
- [Docker](https://docs.docker.com/install/) instalado y funcionando
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) instalado
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) instalado

## Instalación de Kubernetes

Kubernetes se puede instalar en su máquina local usando Minikube. Minikube es una implementación ligera de Kubernetes que se puede usar con fines de desarrollo y prueba.

Para instalar Kubernetes usando Minikube, ejecute el siguiente comando:

```
$ minikube start
```

Esto iniciará una máquina virtual e instalará Kubernetes en ella. Una vez que se completa la instalación, puede verificar la instalación ejecutando el siguiente comando:

```
$ kubectl get nodes
```

Este comando debe enumerar el nodo que creó Minikube.

## Creación de un clúster de Kubernetes

Ahora que Kubernetes está en funcionamiento, puede crear un clúster de Kubernetes. Para hacer esto, deberá crear una [implementación](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) y un [servicio](https://kubernetes.io/docs/concepts /servicios-redes/servicio/).

Una implementación es un objeto de Kubernetes que describe un estado deseado para un grupo de pods. Un servicio es un objeto de Kubernetes que expone un grupo de pods al mundo exterior.

Para crear una implementación y un servicio, deberá crear un archivo [YAML](https://en.wikipedia.org/wiki/YAML) que contenga lo siguiente:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
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
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30000
  selector:
    app: nginx
```

En este archivo, hemos definido una implementación con tres réplicas del contenedor [nginx](https://www.nginx.com/) y un servicio que expone la implementación al mundo exterior.

Para crear la implementación y el servicio, ejecute el siguiente comando:

```
$ kubectl apply -f deployment.yaml
```

Esto creará la implementación y el servicio. Puede verificar que la implementación y el servicio se crearon ejecutando los siguientes comandos:

```
$ kubectl get deployments
```

```
$ kubectl get services
```

## Acceso al clúster de Kubernetes

Ahora que se han creado la implementación y el servicio, puede acceder al clúster de Kubernetes desde su máquina local. Para hacer esto, deberá obtener la dirección IP de la máquina virtual Minikube y el puerto de nodo del servicio.

Para obtener la dirección IP de la máquina virtual Minikube, ejecute el siguiente comando:

```
$ minikube ip
```

Para obtener el puerto de nodo del servicio, ejecute el siguiente comando:

```
$ kubectl describe service nginx-service
```

Debería ver el siguiente resultado:

```
Name:              nginx-service
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=nginx
Type:              NodePort
IP:                10.0.0.1
Port:              <unnamed>  80/TCP
TargetPort:        80/TCP
NodePort:          <unnamed>  30000/TCP
Endpoints:         10.0.0.2:80,10.0.0.3:80,10.0.0.4:80
Session Affinity:  None
External Traffic Policy:  Cluster
Events:            <none>
```

El puerto del nodo es el valor del campo `NodePort`. En este caso, el puerto del nodo es `30000`.

Para acceder al clúster de Kubernetes, abra un navegador web y vaya a `http://<minikube-ip>:<node-port>`. En nuestro ejemplo, la URL sería `http://10.0.0.1:30000`.

Debería ver la página nginx predeterminada:

![nginx](https://www.nginx.com/wp-content/uploads/2018/08/nginx-logo.png)

## Eliminación del clúster de Kubernetes

Para eliminar el clúster de Kubernetes, ejecute el siguiente comando:

```
$ minikube delete
```

Esto eliminará la máquina virtual Minikube y todos los recursos que se crearon en los pasos anteriores.

## Conclusión

En este artículo, le mostramos cómo instalar Kubernetes en su máquina local y crear un clúster de Kubernetes. Kubernetes es una poderosa herramienta que puede ayudarlo a automatizar la implementación, el escalado y la administración de sus aplicaciones en contenedores.