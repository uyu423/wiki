---
title: Contenedorización de Linux con Docker
description: 
published: true
date: 2023-02-12T02:32:22.106Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:32:20.490Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Containerization with Docker***English** document is available*](/en/Knowledge-base/Linux/linux-containerization-with-docker)
{.links-list}


# Contenedorización de Linux con Docker

En este artículo, veremos la creación de contenedores de Linux con Docker. Cubriremos qué son los contenedores, cómo funcionan y por qué es posible que desee usarlos. También repasaremos algunos comandos básicos para trabajar con contenedores Docker. Al final de este artículo, debe tener una buena comprensión de cómo usar Docker para contener sus aplicaciones.

## ¿Qué son los contenedores?

Los contenedores son una forma de aislar su aplicación del resto del sistema. Funcionan empaquetando la aplicación y sus dependencias en una sola unidad que se puede ejecutar en cualquier lugar. Este aislamiento hace que sea mucho más fácil mover su aplicación y garantiza que siempre se ejecutará de la misma manera, sin importar dónde se implemente.

## ¿Cómo funcionan los contenedores?

Los contenedores se construyen sobre una característica del kernel de Linux llamada espacios de nombres. Los espacios de nombres le permiten crear entornos aislados dentro de un solo sistema Linux. Este aislamiento es lo que le permite ejecutar múltiples contenedores en un solo host.

Cada contenedor tiene su propio conjunto de espacios de nombres, lo que le proporciona su propio entorno aislado. Este entorno incluye su propio árbol de procesos, interfaces de red, puntos de montaje y más. Este aislamiento significa que una aplicación en contenedores siempre se ejecutará igual, sin importar dónde se implemente.

## ¿Por qué usar contenedores?

Hay algunas razones por las que es posible que desee utilizar contenedores.

### 1. Portabilidad

Los contenedores son portátiles, lo que significa que se pueden mover fácilmente de un sistema a otro. Esto facilita la implementación de sus aplicaciones en múltiples plataformas.

### 2. Reproducibilidad

Los contenedores también son reproducibles, lo que significa que se pueden recrear fácilmente. Esto es importante para el desarrollo y las pruebas, ya que siempre puede estar seguro de que su aplicación se ejecutará de la misma manera en producción que en su entorno de desarrollo.

### 3. Aislamiento de recursos

Los contenedores brindan aislamiento de recursos, lo que significa que cada contenedor tiene su propio entorno aislado. Este aislamiento garantiza que su aplicación siempre tendrá los recursos que necesita para ejecutarse, independientemente de qué otras aplicaciones se estén ejecutando en el mismo sistema.

## Primeros pasos con Docker

Ahora que hemos cubierto qué son los contenedores y por qué es posible que desee usarlos, echemos un vistazo a cómo usar Docker para contener sus aplicaciones.

Docker es una herramienta que facilita el trabajo con contenedores. Proporciona una interfaz de línea de comandos para gestionar contenedores, así como una plataforma para compartir imágenes de contenedores.

### Instalación de Docker

Antes de que pueda usar Docker, deberá instalarlo en su sistema. Docker está disponible para una variedad de plataformas, incluidas Linux, macOS y Windows.

Para instalar Docker en Ubuntu, puede usar el siguiente comando:

```
sudo apt-get install docker.io
```

Una vez que Docker está instalado, puede usar el comando `docker` para administrar contenedores.

### Creando un contenedor

Para crear un contenedor, puede usar el comando `docker run`. Este comando toma una imagen de contenedor y crea un nuevo contenedor a partir de ella. Por ejemplo, para crear un contenedor a partir de la imagen de Ubuntu, puede usar el siguiente comando:

```
docker run -it ubuntu
```

Este comando extraerá la imagen de Ubuntu de Docker Hub y creará un nuevo contenedor a partir de ella. El indicador `-it` le dice a Docker que ejecute el contenedor en modo interactivo.

Una vez que el contenedor se esté ejecutando, se le colocará en un shell Bash dentro del contenedor. Desde aquí, puede ejecutar los comandos que desee. Cuando haya terminado, puede salir del contenedor escribiendo `exit`.

### Visualización de contenedores

Para ver una lista de todos los contenedores en su sistema, puede usar el comando `docker ps`. Este comando le mostrará los contenedores que se están ejecutando actualmente, así como los contenedores que se han creado pero que no se están ejecutando.

Para ver todos los contenedores, incluidos los que se han creado pero no se están ejecutando, puede usar el indicador `-a`.

### Iniciar y detener contenedores

Para iniciar un contenedor que no se está ejecutando actualmente, puede usar el comando `docker start`. Por ejemplo, para iniciar el contenedor que creamos en la sección anterior, puede usar el siguiente comando:

```
docker start ubuntu
```

Para detener un contenedor que se está ejecutando actualmente, puede usar el comando `docker stop`. Por ejemplo, para detener el contenedor que creamos en la sección anterior, puede usar el siguiente comando:

```
docker stop ubuntu
```

### Eliminación de contenedores

Para eliminar un contenedor, puede usar el comando `docker rm`. Por ejemplo, para eliminar el contenedor que creamos en la sección anterior, puede usar el siguiente comando:

```
docker rm ubuntu
```

## Conclusión

En este artículo, analizamos qué son los contenedores y cómo usar Docker para contener sus aplicaciones. También cubrimos algunos comandos básicos para trabajar con contenedores Docker. Al final de este artículo, debe tener una buena comprensión de cómo usar Docker para contener sus aplicaciones.