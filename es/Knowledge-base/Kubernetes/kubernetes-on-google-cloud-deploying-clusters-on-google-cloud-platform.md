---
title: Kubernetes en Google Cloud: implementación de clústeres en Google Cloud Platform
description: 
published: true
date: 2023-02-14T05:33:12.838Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:33:05.649Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes on Google Cloud: Deploying Clusters on Google Cloud Platform***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-google-cloud-deploying-clusters-on-google-cloud-platform)
{.links-list}


# Kubernetes en Google Cloud: implementación de clústeres en Google Cloud Platform

Kubernetes es un sistema de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores. Agrupa los contenedores que componen una aplicación en unidades lógicas para facilitar la gestión y el descubrimiento. Kubernetes está alojado en Google Cloud Platform (GCP) y se usa para orquestar y administrar contenedores implementados en GCP.

Kubernetes en GCP es una forma escalable, confiable y rentable de implementar sus aplicaciones en contenedores. GCP ofrece muchos beneficios en comparación con otros proveedores de la nube, incluidos precios de pago por uso, facturación por minuto y sin costos iniciales. También puede usar Kubernetes en GCP para administrar sus cargas de trabajo locales.

En este artículo, le mostraremos cómo implementar un clúster de Kubernetes en GCP. También le mostraremos cómo implementar una aplicación simple en su clúster de Kubernetes.

## Requisitos previos

- Una cuenta de Google Cloud
- Un proyecto creado en Google Cloud Console
- La herramienta de línea de comandos de gcloud instalada en su máquina local
- Conocimientos básicos de Kubernetes

## Creación de un clúster de Kubernetes

Un clúster de Kubernetes consta de un conjunto de nodos, cada uno de los cuales es una máquina física o virtual que ejecuta los componentes de Kubernetes. Hay dos tipos de nodos en un clúster de Kubernetes:

- **Nodos maestros**: estos nodos son los responsables de la gestión del clúster de Kubernetes. Proporcionan los componentes del servidor API, el planificador y el administrador del controlador.
- **Nodos trabajadores**: estos nodos ejecutan las aplicaciones que se implementan en el clúster de Kubernetes.

En esta sección, le mostraremos cómo crear un clúster de Kubernetes con tres nodos: un nodo maestro y dos nodos trabajadores.

### Creación del nodo maestro

1. Inicie sesión en Google Cloud Console y vaya a la página **Compute Engine** > **Instancias de VM**.
2. Haga clic en el botón **Crear instancia**.
3. En el campo **Nombre**, ingrese **kubernetes-master**.
4. En el campo **Zona**, seleccione una zona que esté cerca de su ubicación.
5. En el campo **Tipo de máquina**, seleccione **n1-estándar-1**.
6. En la sección **Disco de arranque**, haga clic en **Cambiar**.
7. En la sección **Disco de arranque**, seleccione **Ubuntu 16.04 LTS** de la lista desplegable **Sistema operativo**.
8. En la lista desplegable **Tipo de disco de arranque**, seleccione **SSD (disco persistente)**.
9. En el campo **Tamaño del disco de arranque**, ingrese **10GB**.
10. Haga clic en el botón **Seleccionar**.
11. En la sección **Cortafuegos**, seleccione la casilla de verificación **Permitir tráfico HTTP**.
12. Haga clic en el botón **Crear**.

Su nodo maestro ahora debería estar creado.

### Creando los nodos trabajadores

1. Inicie sesión en Google Cloud Console y vaya a la página **Compute Engine** > **Instancias de VM**.
2. Haga clic en el botón **Crear instancia**.
3. En el campo **Nombre**, ingrese **kubernetes-worker-1**.
4. En el campo **Zona**, seleccione la misma zona que seleccionó para el nodo maestro.
5. En el campo **Tipo de máquina**, seleccione **n1-estándar-1**.
6. En la sección **Disco de arranque**, haga clic en **Cambiar**.
7. En la sección **Disco de arranque**, seleccione **Ubuntu 16.04 LTS** de la lista desplegable **Sistema operativo**.
8. En la lista desplegable **Tipo de disco de arranque**, seleccione **SSD (disco persistente)**.
9. En el campo **Tamaño del disco de arranque**, ingrese **10GB**.
10. Haga clic en el botón **Seleccionar**.
11. En la sección **Cortafuegos**, seleccione la casilla de verificación **Permitir tráfico HTTP**.
12. Haga clic en el botón **Crear**.

Repita los pasos anteriores para crear un segundo nodo trabajador, pero use **kubernetes-worker-2** como nombre para el segundo nodo.

Sus nodos trabajadores ahora deberían estar creados.

## Instalación de Kubernetes

En esta sección, le mostraremos cómo instalar Kubernetes en su nodo maestro.

1. Inicie sesión en su nodo principal mediante SSH.
2. Ejecute el siguiente comando para agregar el repositorio apt de Kubernetes:

```
$ sudo apt-get install -y apt-transport-https
3. Run the following command to add the Kubernetes GPG key:

```
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key agregar -
4. Ejecute el siguiente comando para agregar el repositorio de Kubernetes:

```
$ sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
5. Update the package list:

```
$ sudo apt-obtener actualización
6. Instale Kubernetes:

```
$ sudo apt-get install -y kubelet kubeadm kubectl
7. Once the installation is complete, run the following command to start the Kubernetes master node:

```
$ sudo kubeadm inicio
8. Ejecute el siguiente comando para configurar kubectl:

```
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
9. Your Kubernetes master node should now be up and running.

## Joining Worker Nodes to the Cluster

In this section, we will show you how to join your worker nodes to the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to get the join command:

```
$ sudo kubeadm token create --print-join-command
3. Inicie sesión en sus nodos trabajadores mediante SSH.
4. Ejecute el comando de unión que obtuvo en el paso anterior en cada uno de sus nodos trabajadores.
5. Sus nodos trabajadores ahora deberían unirse al clúster de Kubernetes.

## Implementación de una aplicación

En esta sección, le mostraremos cómo implementar una aplicación simple en su clúster de Kubernetes.

1. Inicie sesión en su nodo principal mediante SSH.
2. Cree un archivo denominado **nginx-deployment.yaml** con el siguiente contenido:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
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
3. Run the following command to deploy the application:

```
$ kubectl create -f nginx-deployment.yaml
4. Ejecute el siguiente comando para enumerar los pods implementados:

```
$ kubectl get pods
5. Run the following command to expose the deployment:

```
$ kubectl expone la implementación nginx-deployment --type=LoadBalancer --port=80 --target-port=80
6. Ejecute el siguiente comando para obtener la URL del servicio:

```
$ kubectl get service nginx-deployment
7. Access the application using the service URL. You should see the default Nginx page.

Your application is now deployed on your Kubernetes cluster.

## Deleting the Cluster

In this section, we will show you how to delete the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to delete the cluster:

```
$ sudo kubeadm restablecer
3. Elimine el nodo principal:

```
$ gcloud compute instances delete kubernetes-master
4. Delete the worker nodes:

```
$ instancias informáticas de gcloud eliminar kubernetes-worker-1
$ instancias informáticas de gcloud eliminar kubernetes-worker-2
5. Su clúster de Kubernetes ahora debería eliminarse.

## Conclusión

En este artículo, le mostramos cómo implementar un clúster de Kubernetes en GCP. También le mostramos cómo implementar una aplicación simple en su clúster de Kubernetes.