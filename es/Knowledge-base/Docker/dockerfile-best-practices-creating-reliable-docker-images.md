---
title: Prácticas recomendadas de Dockerfile: creación de imágenes de Docker fiables
description: 
published: true
date: 2023-02-15T23:32:48.905Z
tags: 
editor: markdown
dateCreated: 2023-02-15T23:32:47.219Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Dockerfile Best Practices: Creating Reliable Docker Images***English** document is available*](/en/Knowledge-base/Docker/dockerfile-best-practices-creating-reliable-docker-images)
{.links-list}


# Prácticas recomendadas de Dockerfile: creación de imágenes de Docker fiables

Los Dockerfiles son una parte fundamental del uso de Docker. Le permiten crear sus propias imágenes, que pueden usarse para crear nuevos contenedores. Un Dockerfile bien diseñado puede facilitar la creación, el mantenimiento y la actualización de sus imágenes, y puede ahorrarle mucho tiempo y esfuerzo a largo plazo.

Este artículo ofrecerá algunas de las mejores prácticas para crear imágenes de Docker confiables, con el objetivo de facilitarle la vida como usuario de Docker.

## Usar .dockerignore

El archivo .dockerignore se usa para especificar archivos y directorios que deben excluirse de su imagen. Esto es útil para excluir archivos que no son necesarios en su imagen, como archivos temporales o artefactos de construcción.

Para crear un archivo .dockerignore, simplemente cree un archivo llamado ".dockerignore" en el directorio raíz de su proyecto y agregue cada archivo o directorio que desee excluir, uno por línea. Por ejemplo:

```
.dockerignore

# Exclude all temporary files
*.tmp

# Exclude all build artifacts
build/
```

## Mantenga su Dockerfile simple

Un Dockerfile simple es más fácil de entender y mantener que uno complejo. También es más probable que sea compatible con futuras versiones de Docker.

Una forma de mantener su Dockerfile simple es evitar el uso de comandos de shell complejos. Si es posible, use imágenes acoplables existentes como base para su propia imagen e instale el software necesario usando un administrador de paquetes como apt o yum.

Otra forma de mantener su Dockerfile simple es evitar instalar software innecesario. Si solo está utilizando una imagen para un propósito específico, no es necesario instalar un sistema operativo completo con un editor de texto, un navegador web, etc.

## Use una etiqueta específica para su imagen base

Cuando utilice una imagen base de un registro de Docker, especifique siempre una etiqueta específica en lugar de utilizar la etiqueta "más reciente". Los desarrolladores suelen utilizar la etiqueta "más reciente" para indicar la versión de desarrollo más reciente de una imagen, que podría no ser adecuada para su uso en producción.

## Usar una sola instrucción RUN

Si es posible, use una sola instrucción RUN en su Dockerfile en lugar de varias instrucciones. Esto hará que su imagen sea más fácil de construir y reducirá la cantidad de capas en su imagen, lo que puede ser importante para el rendimiento.

Para usar una sola instrucción RUN, simplemente combine todos los comandos que desea ejecutar en una sola línea, separados por &&. Por ejemplo:

```
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:my-ppa && \
    apt-get update && \
    apt-get install -y my-software
```

## Usar un usuario específico

De forma predeterminada, los contenedores se ejecutan como usuario raíz. Esto puede ser un riesgo para la seguridad, ya que cualquier proceso que se ejecute en el contenedor tendrá acceso completo a la máquina host.

Para evitar esto, puede crear un nuevo usuario en su Dockerfile y usar este usuario para ejecutar cualquier proceso en el contenedor. Por ejemplo:

```
# Create a new user
RUN useradd -ms /bin/bash myuser

# Use the new user for all subsequent commands
USER myuser
```

## Usar un directorio de trabajo específico

Cuando se crea un contenedor, se le asigna un directorio de trabajo predeterminado. Este directorio se puede anular mediante la instrucción WORKDIR en su Dockerfile.

Es una buena idea especificar un directorio de trabajo específico, ya que puede facilitar la búsqueda de archivos en su contenedor y puede ayudar con la portabilidad entre diferentes máquinas. Por ejemplo:

```
# Set the working directory to /app
WORKDIR /app
```

## Evite usar AGREGAR y COPIAR

Las instrucciones ADD y COPY son similares, pero hay algunas diferencias importantes entre ellas. ADD se puede usar para extraer archivos de una URL remota, mientras que COPY solo se puede usar para copiar archivos del contexto de compilación.

ADD también es más poderoso que COPY, ya que puede resolver automáticamente las dependencias entre archivos. Por ejemplo, si AGREGAR un archivo .tar.gz, AGREGAR extraerá automáticamente los archivos del archivo.

Debido a estas diferencias, generalmente se recomienda usar COPY en lugar de ADD en su Dockerfile.

## Especifique un control de salud

Una comprobación de estado es una prueba que se utiliza para determinar si un contenedor está en buen estado y si debe seguir ejecutándose. Si falla una verificación de estado, el contenedor se detendrá y se reiniciará.

Las comprobaciones de estado se pueden especificar mediante la instrucción HEALTHCHECK en su Dockerfile. Por ejemplo:

```
# Check that the container is healthy every 30 seconds
# and that the HTTP service is responding on port 80
HEALTHCHECK --interval=30s --timeout=5s \
    CMD wget -qO- http://localhost:80/ || exit 1
```

## Usar compilaciones de varias etapas

Las compilaciones de varias etapas son una característica de Docker que le permite crear varias imágenes como parte de un único proceso de compilación. Esto puede ser útil para crear imágenes más pequeñas y seguras, ya que puede eliminar archivos innecesarios de su imagen después de crearla.

Para usar compilaciones de varias etapas, simplemente cree varias instrucciones FROM en su Dockerfile, cada una con un nombre de imagen diferente. Por ejemplo:

```
# Build stage
FROM golang:1.8 as builder

WORKDIR /src

COPY . .

RUN go build -o app

# Run stage
FROM alpine:latest

WORKDIR /app

COPY --from=builder /src/app .

CMD ["./app"]
```

## Conclusión

Si sigue las mejores prácticas descritas en este artículo, puede hacer que sus Dockerfiles sean más confiables, más fáciles de entender y más fáciles de mantener. Esto le ahorrará tiempo y esfuerzo a largo plazo y hará que su vida como usuario de Docker sea mucho más fácil.