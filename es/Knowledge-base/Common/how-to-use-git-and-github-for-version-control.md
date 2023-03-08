---
title: Cómo usar Git y GitHub para el control de versiones
description: 
published: true
date: 2023-02-02T06:29:46.533Z
tags: 
editor: markdown
dateCreated: 2023-02-02T06:23:35.070Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Use Git and GitHub for Version Control***English** document is available*](/en/Knowledge-base/Common/how-to-use-git-and-github-for-version-control)
{.links-list}


# Cómo usar Git y GitHub para el control de versiones

Git es una poderosa herramienta para desarrolladores que les permite realizar un seguimiento de los cambios en su código, trabajar con otros en proyectos colaborativos y compartir su código con el mundo. GitHub es un popular servicio en línea para hospedar y administrar repositorios de Git. En este artículo, le mostraremos cómo usar Git y GitHub para el control de versiones.

## ¿Qué es el control de versiones?

El control de versiones es un sistema que realiza un seguimiento de los cambios en los archivos a lo largo del tiempo. Esto es útil para los desarrolladores porque les permite deshacer cambios, experimentar con nuevas funciones y colaborar con otros en proyectos de código.

## ¿Qué es Git?

Git es un sistema de control de versiones que fue creado por Linus Torvalds, el creador del sistema operativo Linux. Git es una herramienta gratuita y de código abierto muy utilizada por los desarrolladores.

## ¿Qué es GitHub?

GitHub es un popular servicio en línea para hospedar y administrar repositorios de Git. GitHub facilita la colaboración en proyectos de código y el seguimiento de cambios en su código.

## Cómo usar Git y GitHub para el control de versiones

En esta sección, le mostraremos cómo usar Git y GitHub para el control de versiones.

### Cómo instalar Git

Git es una herramienta gratuita y de código abierto que se puede descargar desde el [sitio web de Git] (https://git-scm.com/). Para instalar Git, siga las instrucciones para su sistema operativo:

- [Windows](https://git-scm.com/downloads/windows)
- [macOS](https://git-scm.com/downloads/mac)
- [Linux](https://git-scm.com/downloads/linux)

### Cómo crear un repositorio Git

Un repositorio de Git es una colección de archivos que son rastreados por Git. Para crear un nuevo repositorio Git, use el comando `git init`:

```
$ git init
```

### Cómo agregar archivos a un repositorio Git

Una vez que haya creado un repositorio de Git, puede agregarle archivos usando el comando `git add`. Para agregar un archivo a un repositorio de Git, use el comando `git add` seguido de la ruta al archivo:

```
$ git add filename
```

También puede agregar todos los archivos modificados y sin seguimiento en un directorio a un repositorio de Git usando el comando `git add` con la opción `-A`:

```
$ git add -A
```

### Cómo realizar cambios en un repositorio de Git

Una vez que haya agregado archivos a un repositorio de Git, puede confirmar esos cambios en el repositorio usando el comando `git commit`. Para confirmar cambios en un repositorio de Git, use el comando `git commit` seguido de un mensaje que describe los cambios:

```
$ git commit -m "message"
```

### Cómo enviar cambios a un repositorio Git remoto

Una vez que haya realizado cambios en un repositorio de Git, puede enviar esos cambios a un repositorio remoto usando el comando `git push`. Para enviar cambios a un repositorio Git remoto, use el comando `git push` seguido del nombre del repositorio remoto:

```
$ git push origin
```

### Cómo crear un repositorio de GitHub

GitHub es un popular servicio en línea para hospedar y administrar repositorios de Git. Para crear un nuevo repositorio de GitHub, regístrese para obtener una cuenta de GitHub y luego cree un nuevo repositorio desde el sitio web de GitHub.

### Cómo enviar un repositorio Git existente a GitHub

Si tiene un repositorio Git existente, puede enviarlo a GitHub usando el comando `git push`. Para enviar un repositorio Git existente a GitHub, use el comando `git push` seguido de la opción `-u` y el nombre del repositorio remoto:

```
$ git push -u origin
```

### Cómo extraer cambios de un repositorio Git remoto

Si tiene un repositorio Git remoto, puede extraer cambios de ese repositorio usando el comando `git pull`. Para extraer cambios de un repositorio Git remoto, use el comando `git pull` seguido del nombre del repositorio remoto:

```
$ git pull origin
```

## Conclusión

En este artículo, le mostramos cómo usar Git y GitHub para el control de versiones. Git es una poderosa herramienta para desarrolladores que les permite realizar un seguimiento de los cambios en su código, trabajar con otros en proyectos colaborativos y compartir su código con el mundo. GitHub es un popular servicio en línea para hospedar y administrar repositorios de Git.