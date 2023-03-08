---
title: Kubernetes con Containerd: ejecución de contenedores con otro tiempo de ejecución de contenedores
description: 
published: true
date: 2023-02-14T10:32:36.204Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:32:28.855Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with Containerd: Running Containers with Another Container Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-containerd-running-containers-with-another-container-runtime)
{.links-list}


# Kubernetes con Containerd: ejecución de contenedores con otro tiempo de ejecución de contenedores

El tiempo de ejecución de contenedor predeterminado para Kubernetes es Docker, pero Kubernetes también es compatible con otros tiempos de ejecución de contenedor. En este artículo, veremos cómo ejecutar Kubernetes con Containerd.

## ¿Por qué usar contenedores?

Containerd es un tiempo de ejecución de contenedor estándar de la industria que es popular por su simplicidad y solidez. También lo utilizan otras plataformas de orquestación de contenedores, como Docker Swarm y Apache Mesos.

## Instalación de contenedores

Para instalar Containerd, puede usar un administrador de paquetes como apt o yum.

```
sudo apt install containerd
```

## Configuración de Kubernetes para usar Containerd

Una vez que Containerd está instalado, debe configurar Kubernetes para usarlo como tiempo de ejecución del contenedor. Para hacer esto, debe editar el archivo `/etc/kubernetes/manifests/kubelet.yaml` y agregar la siguiente línea:

```
--container-runtime=containerd
```

También debe editar el archivo `/etc/systemd/system/kubelet.service.d/10-kubelet.conf` y agregar la siguiente línea:

```
Environment="KUBELET_EXTRA_ARGS=--container-runtime=containerd"
```

Después de realizar estos cambios, debe reiniciar el servicio `kubelet`.

```
sudo systemctl restart kubelet
```

## Crear un contenedor

Ahora que Kubernetes está configurado para usar Containerd, creemos un contenedor.

Primero, necesitamos crear un archivo llamado `container.json` con los siguientes contenidos:

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest"
}
```

A continuación, necesitamos crear el contenedor usando el comando `ctr`.

```
sudo ctr create -f container.json
```

## Ejecutar un contenedor

Ahora que hemos creado un contenedor, vamos a ejecutarlo.

Primero, necesitamos crear un archivo llamado `run.json` con los siguientes contenidos:

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest",
  "command": ["nginx", "-g", "daemon off;"]
}
```

A continuación, necesitamos ejecutar el contenedor usando el comando `ctr`.

```
sudo ctr run -f run.json
```

## Eliminación de un contenedor

Para eliminar un contenedor, podemos usar el comando `ctr`.

```
sudo ctr delete container1
```

## Conclusión

En este artículo, hemos visto cómo usar Kubernetes con Containerd. También hemos visto cómo instalar Containerd, configurar Kubernetes para usarlo y cómo crear y ejecutar contenedores.