---
title: Kubernetes en Azure: implementación de clústeres en Microsoft Azure
description: 
published: true
date: 2023-02-01T16:17:59.838Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:17:58.198Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [Kubernetes on Azure: Deploying Clusters on Microsoft Azure***Spanish** version of this document is available*](/es/Knowledge-base/Kubernetes/kubernetes-on-azure-deploying-clusters-on-microsoft-azure)
{.links-list}


# Kubernetes en Azure: implementación de clústeres en Microsoft Azure

Kubernetes es un sistema de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores. Agrupa los contenedores que componen una aplicación en unidades lógicas para facilitar la gestión y el descubrimiento. Microsoft Azure ofrece un servicio de Kubernetes administrado llamado Azure Kubernetes Service (AKS) que agiliza y facilita la implementación de un clúster de Kubernetes listo para producción en Azure.

En este artículo, le mostraremos cómo implementar un clúster de Kubernetes en Azure mediante AKS. También le mostraremos cómo implementar una aplicación simple en el clúster y exponerla en Internet.

## Requisitos previos

Antes de comenzar, necesitará lo siguiente:

- Una cuenta de Azure. Si no tiene uno, puede registrarse para una prueba gratuita.
- La CLI de Azure instalada en su máquina local.
- La herramienta de línea de comandos kubectl.

## Creación de un clúster de AKS

El primer paso es crear un clúster de AKS mediante la CLI de Azure. Usaremos el comando az aks create para crear un grupo de recursos, un clúster de AKS y generar un archivo kubeconfig. La herramienta kubectl utiliza el archivo kubeconfig para conectarse al clúster de Kubernetes.

Ejecute el siguiente comando para crear un clúster de AKS:

```
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 3 \
  --generate-ssh-keys
```

El clúster de AKS tardará unos minutos en crearse. Una vez que esté listo, puede usar la herramienta kubectl para conectarse al clúster.

## Conexión al clúster

Para conectarse al clúster de AKS, debe recuperar las credenciales del clúster de Azure y configurar kubectl para usarlas.

Ejecute el siguiente comando para recuperar las credenciales:

```
az aks get-credentials \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

Esto descargará un archivo kubeconfig y lo fusionará con el archivo kubeconfig existente en su máquina.

Ahora puede usar la herramienta kubectl para interactuar con el clúster de AKS. Ejecute el siguiente comando para obtener una lista de los nodos en el clúster:

```
kubectl get nodes
```

## Implementación de una aplicación

Ahora que tenemos un clúster de Kubernetes en funcionamiento, podemos implementar una aplicación en él. Para este ejemplo, implementaremos una aplicación web simple escrita en Node.js.

Primero, necesitamos crear una imagen Docker de la aplicación. Usaremos el Dockerfile en el directorio raíz del proyecto para construir la imagen. Ejecute el siguiente comando para construir la imagen:

```
docker build -t my-app:v1 .
```

Una vez que se ha creado la imagen, podemos enviarla a un registro de Docker. Para este ejemplo, lo enviaremos a Azure Container Registry (ACR).

Primero, necesitamos crear una instancia de ACR. Podemos usar el comando az acr create para hacer esto. Ejecute el siguiente comando para crear una instancia de ACR:

```
az acr create \
  --resource-group myResourceGroup \
  --name myACR \
  --sku Basic
```

Una vez que se ha creado la instancia de ACR, podemos enviarle la imagen de Docker. Ejecute el siguiente comando para enviar la imagen:

```
docker push myacr.azurecr.io/my-app:v1
```

Ahora que la imagen se envió a ACR, podemos implementarla en nuestro clúster de AKS. Usaremos una implementación de Kubernetes para hacer esto. Una implementación es un recurso que administra un conjunto de réplicas de un pod. El pod es la unidad básica de implementación en Kubernetes. Es un grupo de uno o más contenedores que se implementan juntos en el mismo host.

Usaremos la herramienta kubectl para crear la implementación. Ejecute el siguiente comando para crear la implementación:

```
kubectl create deployment my-app --image=myacr.azurecr.io/my-app:v1
```

Esto creará una implementación llamada my-app que administrará un conjunto de réplicas de pods. Los pods se crearán a partir de la imagen my-app:v1 que enviamos a ACR.

Podemos usar el comando kubectl get deployments para ver la implementación que acabamos de crear:

```
kubectl get deployments
```

También podemos usar el comando kubectl get pods para ver los pods administrados por la implementación:

```
kubectl get pods
```

## Exponiendo la aplicación

Ahora que nuestra aplicación está implementada, debemos exponerla a Internet para que los usuarios puedan acceder a ella. Podemos hacer esto creando un servicio de Kubernetes. Un servicio es una abstracción que define un conjunto lógico de pods y una política mediante la cual acceder a ellos.

Crearemos un servicio de tipo LoadBalancer. Esto creará un equilibrador de carga en Azure y lo asignará a los pods administrados por la implementación de my-app.

Ejecute el siguiente comando para crear el servicio:

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=8080
```

Esto creará un servicio llamado my-app que expone el puerto 80 en el balanceador de carga. El tráfico a este puerto se reenviará al puerto 8080 en los pods administrados por la implementación de my-app.

Podemos usar el comando kubectl get services para ver el servicio que acabamos de crear:

```
kubectl get services
```

Una vez que se ha creado el servicio, el balanceador de carga tardará unos minutos en aprovisionarse y en asignar una dirección IP pública al servicio. Puede usar el comando kubectl get services para ver el estado del servicio:

```
kubectl get services
```

Una vez que se ha creado el servicio, puede usar la dirección IP pública para acceder a la aplicación en un navegador web.

## Eliminación del clúster

Si ya no necesita el clúster de AKS, puede eliminarlo para dejar de incurrir en cargos. Para eliminar el clúster, ejecute el siguiente comando:

```
az aks delete \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

## Conclusión

En este artículo, le mostramos cómo implementar un clúster de Kubernetes en Azure mediante AKS. También le mostramos cómo implementar una aplicación simple en el clúster y exponerla en Internet.