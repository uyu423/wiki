---
title: Kubernetes en Bare Metal: Implementación de clústeres en servidores físicos
description: 
published: true
date: 2023-02-14T08:33:07.782Z
tags: 
editor: markdown
dateCreated: 2023-02-14T08:33:06.025Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes on Bare Metal: Deploying Clusters on Physical Servers***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-bare-metal-deploying-clusters-on-physical-servers)
{.links-list}


# Kubernetes en Bare Metal: implementación de clústeres en servidores físicos

Hoy en día, los contenedores se utilizan cada vez más para empaquetar e implementar aplicaciones. Esto se debe a que los contenedores ofrecen muchos beneficios sobre las máquinas virtuales tradicionales, como ser más portátiles, ocupar menos espacio y poder iniciarse más rápido.

Kubernetes es una herramienta popular de orquestación de contenedores que se puede usar para administrar grandes cantidades de contenedores. Kubernetes se usa a menudo con soluciones basadas en la nube, pero también se puede implementar en servidores bare metal.

La implementación de Kubernetes en servidores bare metal puede ofrecer algunas ventajas sobre su uso con una solución basada en la nube. Por ejemplo, puede ser más rentable y tiene más control sobre el hardware.

En este artículo, veremos cómo implementar un clúster de Kubernetes en servidores bare metal. También veremos algunos de los desafíos que puede enfrentar al hacer esto.

## Descripción general

Antes de comenzar, echemos un vistazo rápido a algunos de los conceptos clave que usaremos en este artículo.

**Kubernetes**: Kubernetes es una herramienta de orquestación de contenedores que se puede usar para administrar una gran cantidad de contenedores.

**Servidor bare metal**: un servidor bare metal es un servidor físico que no tiene una capa de virtualización.

**Cluster**: un clúster es un grupo de servidores que se utilizan para ejecutar una aplicación o un servicio.

**Nodo maestro**: el nodo maestro es el servidor que se usa para administrar el clúster de Kubernetes.

**Nodo trabajador**: los nodos trabajadores son los servidores que se utilizan para ejecutar los contenedores.

## Requisitos previos

Antes de comenzar, necesitará tener los siguientes elementos:

- Un grupo de servidores bare metal. Para este artículo, utilizaremos tres servidores.
- Un conmutador de red al que se pueden conectar los servidores.
- Una forma de instalar Kubernetes en los servidores. Para este artículo, usaremos el instalador de Kubernetes, kubeadm.

## Instalación de Kubernetes

En esta sección, veremos cómo instalar Kubernetes en los servidores. Usaremos el instalador de Kubernetes, kubeadm.

Kubeadm es una herramienta que se puede utilizar para instalar y configurar Kubernetes. Está diseñado para ser fácil de usar y fácil de extender.

### Instalación de kubeadm

Lo primero que debemos hacer es instalar kubeadm en los servidores. Esto lo podemos hacer con el siguiente comando:

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update && sudo apt-get install -y kubeadm
```

### Inicializando el nodo maestro

Una vez instalado kubeadm, podemos inicializar el nodo maestro. Este es el servidor que se usará para administrar el clúster de Kubernetes.

Para inicializar el nodo maestro, necesitamos usar el comando kubeadm init. Este comando iniciará un plano de control de Kubernetes en el servidor.

```
sudo kubeadm init
```

Una vez que el comando se haya completado, verá un mensaje similar a este:

```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following commands:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

Deberá ejecutar los comandos que se enumeran en el resultado para configurar su servidor para usar el clúster de Kubernetes.

### Unirse a los nodos trabajadores

Ahora que el nodo maestro está en funcionamiento, podemos agregar nodos trabajadores al clúster. Los nodos trabajadores son los servidores que se utilizan para ejecutar los contenedores.

Para agregar un nodo trabajador al clúster, debemos usar el comando kubeadm join. Este comando agregará el servidor al clúster de Kubernetes.

```
sudo kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

## Configuración del clúster

En esta sección, veremos cómo configurar el clúster de Kubernetes.

### Configuración del nodo maestro

Lo primero que debemos hacer es configurar el nodo maestro. Esto lo podemos hacer ejecutando el siguiente comando:

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

Este comando creará una red de pod en el servidor. Una red de pods es una red que se utiliza para conectar los contenedores.

### Configuración de los nodos trabajadores

A continuación, debemos configurar los nodos trabajadores. Podemos hacer esto ejecutando el siguiente comando en cada nodo trabajador:

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

Este comando creará una red de pod en el servidor. Una red de pods es una red que se utiliza para conectar los contenedores.

## Implementación de una aplicación

En esta sección, veremos cómo implementar una aplicación en el clúster de Kubernetes.

Usaremos el archivo nginx-deployment.yaml que se encuentra en el directorio de ejemplos. Este archivo contiene la configuración para una implementación de nginx.

Para implementar la aplicación, necesitamos ejecutar el siguiente comando:

```
kubectl apply -f examples/nginx-deployment.yaml
```

Este comando creará una implementación en el clúster de Kubernetes. Una implementación es un grupo de conjuntos de réplicas. Un conjunto de réplicas es un grupo de pods.

## Acceso a la aplicación

En esta sección, veremos cómo acceder a la aplicación que implementamos.

Para acceder a la aplicación, necesitamos crear un recurso de ingreso. Un recurso de entrada es un recurso que se utiliza para enrutar el tráfico a la aplicación.

Podemos crear un recurso de ingreso ejecutando el siguiente comando:

```
kubectl apply -f examples/nginx-ingress.yaml
```

Este comando creará un recurso de ingreso en el clúster de Kubernetes.

Una vez creado el recurso de ingreso, podemos acceder a la aplicación dirigiéndonos a la siguiente URL:

http://<IP del clúster>

## Eliminación del clúster

En esta sección, veremos cómo eliminar el clúster de Kubernetes.

Para eliminar el clúster, debemos usar el comando kubectl delete. Este comando eliminará todos los recursos del clúster.

```
kubectl delete -f examples/nginx-deployment.yaml
kubectl delete -f examples/nginx-ingress.yaml
```

## Conclusión

En este artículo, hemos analizado cómo implementar un clúster de Kubernetes en servidores bare metal. También hemos analizado cómo implementar una aplicación en el clúster.