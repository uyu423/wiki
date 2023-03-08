---
title: Kubernetes en OpenStack: implementación de clústeres en OpenStack
description: 
published: true
date: 2023-02-14T06:32:48.795Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:32:47.090Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes on OpenStack: Deploying Clusters on OpenStack***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-openstack-deploying-clusters-on-openstack)
{.links-list}


# Kubernetes en OpenStack: implementación de clústeres en OpenStack

OpenStack es un sistema operativo en la nube que controla grandes grupos de recursos informáticos, de almacenamiento y de red en un centro de datos, todo administrado a través de un tablero que brinda control a los administradores y permite a sus usuarios aprovisionar recursos a través de una interfaz web.

Kubernetes es un sistema de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores.

El objetivo de este artículo es mostrarle cómo implementar un clúster de Kubernetes en OpenStack. Cubriremos los siguientes temas:

- Requisitos previos
- Creación de un clúster de Kubernetes
- Implementación de una aplicación en el clúster

## Requisitos previos

Para seguir esta guía, necesitará lo siguiente:

- Una nube OpenStack con lo siguiente:
  - Una red
  - Un enrutador
  - Una subred
  - Un grupo de seguridad
  - Un par de llaves
  - Al menos 3 nodos de cómputo
- La CLI de OpenStack instalada y configurada
- La CLI de Kubernetes instalada y configurada

## Creación de un clúster de Kubernetes

Usaremos el script `kube-up.sh` para implementar un clúster de Kubernetes. Este script creará todos los recursos necesarios en OpenStack, incluidas instancias informáticas, redes y balanceadores de carga.

Primero, clone el repositorio de Kubernetes:

```
git clone https://github.com/kubernetes/kubernetes.git
```

A continuación, cambie al directorio `kubernetes/cluster/openstack`:

```
cd kubernetes/cluster/openstack
```

Luego, crea un archivo llamado `cloud-config.yaml` con el siguiente contenido:

```yaml
#cloud-config

write_files:
- owner: root:root
  path: /etc/kubernetes/kube-up-config.yaml
  content: |
    CLOUD_PROVIDER=openstack
    OPENSTACK_AUTH_URL=https://identity.example.com:5000/v3
    OPENSTACK_USERNAME=admin
    OPENSTACK_PASSWORD=admin
    OPENSTACK_TENANT_NAME=admin
    OPENSTACK_REGION=regionOne
    OPENSTACK_CLUSTER_NAME=kubernetes
    OPENSTACK_CLUSTER_SIZE=3
    OPENSTACK_MASTER_FLAVOR=m1.small
    OPENSTACK_MASTER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_WORKER_FLAVOR=m1.small
    OPENSTACK_WORKER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_NETWORK_NAME=kubernetes
    OPENSTACK_MASTER_OS_DISTRIBUTION=ubuntu
    OPENSTACK_WORKER_OS_DISTRIBUTION=ubuntu
```

Reemplace los valores de este archivo con sus propias credenciales y configuraciones de OpenStack.

Ahora, puede implementar el clúster ejecutando el script `kube-up.sh`:

```
./kube-up.sh
```

Esto tardará unos minutos en completarse. Una vez que haya terminado, debería ver 3 instancias informáticas en su panel de OpenStack, junto con una red, un enrutador y un equilibrador de carga.

## Implementación de una aplicación en el clúster

Ahora que tenemos un clúster de Kubernetes en funcionamiento en OpenStack, implementemos una aplicación simple en él. Usaremos una imagen de contenedor preconstruida para una aplicación web "Hello, World".

Primero, necesitamos crear un archivo llamado `hello-world.yaml` con los siguientes contenidos:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: tutum/hello-world
        ports:
        - containerPort: 80
```

Este archivo define una implementación denominada "hello-world" con 3 pods de réplica. Los pods se crearán a partir de la imagen del contenedor `tutum/hello-world`, que es una aplicación web simple "Hello, World". Los pods estarán expuestos en el puerto 80.

Ahora podemos implementar esta aplicación ejecutando el siguiente comando:

```
kubectl create -f hello-world.yaml
```

Esto tomará unos segundos para crear los pods. Una vez que están en funcionamiento, podemos exponerlos al mundo exterior mediante la creación de un servicio:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: hello-world
```

Guarde este archivo como `hello-world-service.yaml` e impleméntelo con el siguiente comando:

```
kubectl create -f hello-world-service.yaml
```

Esto creará un balanceador de carga y expondrá el servicio en el puerto 80. Puede encontrar la dirección IP pública del balanceador de carga ejecutando el siguiente comando:

```
kubectl get service hello-world
```

Debería ver una salida similar a la siguiente:

```
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)        AGE
hello-world  LoadBalancer   10.0.0.1        1.2.3.4           80:31527/TCP   1m
```

Ahora puede acceder a la aplicación web "Hello, World" visitando la dirección IP pública del equilibrador de carga en su navegador web.

## Conclusión

En este artículo, le mostramos cómo implementar un clúster de Kubernetes en OpenStack. También le mostramos cómo implementar una aplicación web simple en el clúster.

Para leer más, consulte los siguientes recursos:

- [Kubernetes en OpenStack: una arquitectura de referencia](https://www.openstack.org/assets/pdf/kubernetes-on-openstack-a-reference-architecture.pdf)
- [Implementación de Kubernetes en OpenStack](https://www.mirantis.com/blog/deploying-kubernetes-on-openstack/)
- [Kubernetes de la manera difícil] (https://github.com/kelseyhightower/kubernetes-the-hard-way)