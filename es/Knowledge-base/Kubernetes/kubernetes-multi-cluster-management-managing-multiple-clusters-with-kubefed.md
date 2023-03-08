---
title: Gestión de varios clústeres de Kubernetes: gestión de varios clústeres con kubefed
description: 
published: true
date: 2023-02-14T04:32:31.803Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:32:29.983Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Multi-Cluster Management: Managing Multiple Clusters with kubefed***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-multi-cluster-management-managing-multiple-clusters-with-kubefed)
{.links-list}



# Gestión de múltiples clústeres de Kubernetes: gestión de múltiples clústeres con kubefed

En un entorno de producción, no es raro tener varios clústeres de Kubernetes. Esto puede deberse a una variedad de razones, que incluyen escalamiento, alta disponibilidad o diferentes equipos que trabajan en diferentes proyectos.

Administrar múltiples clústeres de Kubernetes puede ser un desafío, especialmente cuando se trata de mantenerlos sincronizados. Hay algunas opciones para administrar varios clústeres de Kubernetes, pero en este artículo nos centraremos en kubefed.

kubefed es una herramienta que se puede usar para administrar múltiples clústeres de Kubernetes. Forma parte del proyecto Kubernetes y está diseñado para facilitar la creación y el mantenimiento de una federación de clústeres de Kubernetes.

kubefed tiene algunas dependencias, que incluyen:

- kubectl
- kube-apiserver
- kube-controller-manager

kubefed también requiere un clúster de Kubernetes que cumpla con los siguientes requisitos:

- Kubernetes versión 1.4 o superior
- El clúster debe tener habilitado RBAC

## Creación de un clúster de kubefed

Crear un clúster de kubefed es fácil. Primero, necesitamos crear un ConfigMap que se usará para almacenar la configuración de kubefed. Llamaremos a este ConfigMap "kubefed-config":

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: kubefed-config
  namespace: kube-system
data:
  kubefed.yaml: |
    apiVersion: federation/v1beta1
    kind: Federation
    metadata:
      name: federation
    spec:
      # Add clusters to the federation here.
      clusters:
      - clusterName: cluster1
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.1.1:6443
      - clusterName: cluster2
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.2.1:6443
    ```

Este ConfigMap define dos clústeres de Kubernetes que queremos agregar a nuestra federación. Las entradas "cluster1" y "cluster2" en la lista de "clusters" son los nombres de los clústeres que queremos agregar. La entrada "serverAddressByClientCIDRs" define la URL del servidor de la API de Kubernetes para cada clúster.

A continuación, debemos crear un secreto que se usará para almacenar los archivos kubeconfig para cada clúster. Llamaremos a este Secreto "kubefed-kubeconfig":

```
apiVersion: v1
kind: Secret
metadata:
  name: kubefed-kubeconfig
  namespace: kube-system
data:
  kubeconfig-cluster1: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.1.1:6443
        name: cluster1
      name: cluster1
    contexts:
    - context:
        cluster: cluster1
        user: admin
      name: cluster1
    current-context: cluster1
    preferences: {}
    users:
    - name: admin
      user:
        token: abcdefg
  kubeconfig-cluster2: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.2.1:6443
        name: cluster2
      name: cluster2
    contexts:
    - context:
        cluster: cluster2
        user: admin
      name: cluster2
    current-context: cluster2
    preferences: {}
    users:
    - name: admin
      user:
        token: hijklmnop
    ```

Este secreto contiene los archivos kubeconfig para cada clúster. El archivo kubeconfig para cluster1 se almacena en la clave "kubeconfig-cluster1" y el archivo kubeconfig para cluster2 se almacena en la clave "kubeconfig-cluster2".

Con ConfigMap y Secret en su lugar, ahora podemos crear el clúster de kubefed. Usaremos el comando kubectl para crear el clúster kubefed:

```
kubectl create -f kubefed-configmap.yaml
kubectl create -f kubefed-secret.yaml
kubectl create -f kubefed-cluster.yaml
```

Esto creará un nuevo clúster de Kubernetes llamado "kubefed". Este clúster se usará para administrar los otros dos clústeres de Kubernetes que definimos en ConfigMap y Secret.

## Adición de clústeres a kubefed

Ahora que tenemos un clúster de Kubefed, podemos agregarle nuestros otros clústeres de Kubernetes. Usaremos el comando kubefed para agregar los clústeres:

```
kubefed join cluster1 --host-cluster-context=cluster1 --cluster-context=cluster1
kubefed join cluster2 --host-cluster-context=cluster2 --cluster-context=cluster2
```

Esto agregará los clústeres de Kubernetes "cluster1" y "cluster2" al clúster kubefed. Los argumentos "--host-cluster-context" y "--cluster-context" especifican los contextos de kubeconfig que se usarán para el clúster de host (kubefed) y el clúster que se agrega (cluster1 o cluster2).

## Administrar kubefed

Ahora que tenemos nuestro clúster de Kubefed en funcionamiento, podemos comenzar a usarlo para administrar nuestros otros clústeres de Kubernetes.

El comando kubefed se puede usar para administrar kubefed y los clústeres de Kubernetes que administra.

Para enumerar los clústeres de Kubernetes que administra kubefed, use el comando "kubefed list":

```
kubefed list
```

Esto mostrará una lista de los clústeres de Kubernetes que kubefed está administrando actualmente.

Para obtener más información sobre un clúster de Kubernetes en particular, use el comando "kubefed describe":

```
kubefed describe cluster1
```

Esto proporcionará más información sobre el clúster de Kubernetes "cluster1".

El comando kubefed también se puede usar para escalar un clúster de Kubernetes. Para escalar un clúster, use el comando "kubefed scale":

```
kubefed scale cluster1 --replicas=3
```

Esto escalará el clúster de Kubernetes "cluster1" a tres réplicas.

## Eliminación de un clúster de kubefed

Cuando haya terminado con un clúster de kubefed, puede eliminarlo con el comando "eliminar de kubefed":

```
kubefed delete cluster1
```

Esto eliminará el clúster de Kubernetes "cluster1" de kubefed.

## Conclusión

kubefed es una herramienta valiosa para administrar múltiples clústeres de Kubernetes. Es fácil de usar y puede ayudarlo a mantener sus clústeres sincronizados.