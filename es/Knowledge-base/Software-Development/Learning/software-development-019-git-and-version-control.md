---
title: Desarrollo de software 019: Git y control de versiones
description: 
published: true
date: 2023-02-13T08:56:32.789Z
tags: 
editor: markdown
dateCreated: 2023-02-13T08:56:31.066Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 019: Git and Version Control***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-019-git-and-version-control)
{.links-list}


# Desarrollo de Software 019: Git y Control de Versiones

## ¿Qué es Git?

Git es un sistema de control de versiones distribuido gratuito y de código abierto diseñado para manejar todo, desde proyectos pequeños hasta proyectos muy grandes, con rapidez y eficiencia.

## ¿Qué es el control de versiones?

El control de versiones es un sistema que registra los cambios en un archivo o conjunto de archivos a lo largo del tiempo para que pueda recuperar versiones específicas más adelante. Por ejemplo, cuando está desarrollando una pieza de software, es posible que desee guardar diferentes versiones de su código mientras trabaja. Los sistemas de control de versiones le permiten hacer esto.

## ¿Por qué usar Git?

Hay muchas razones para usar Git para el control de versiones. Git es rápido, escalable y tiene una gran comunidad de usuarios. Git también es fácil de aprender y tiene una excelente documentación.

## Cómo usar Git

Git es una herramienta de línea de comandos, pero hay muchas interfaces gráficas de usuario (GUI) que proporcionan una representación gráfica del flujo de trabajo de Git. Usaremos la línea de comando en este tutorial, pero no dude en usar una GUI si lo prefiere.

## Instalación de Git

Git está disponible para todos los principales sistemas operativos. Visite el [sitio web de Git](https://git-scm.com/) para descargar e instalar Git.

## Configurando Git

Antes de poder usar Git, debe configurarlo. Ejecute el siguiente comando para establecer su nombre de usuario:

```
git config --global user.name "Your Name"
```

Reemplace "Su nombre" con su nombre real.

A continuación, configure su dirección de correo electrónico:

```
git config --global user.email "your_email@example.com"
```

Reemplace "your_email@example.com" con su dirección de correo electrónico real.

Finalmente, configure su editor de texto predeterminado:

```
git config --global core.editor nano
```

Puede reemplazar "nano" con su editor de texto preferido.

## Crear un repositorio Git

Un repositorio de Git es una colección de archivos y el historial de cambios en esos archivos. Puede crear un nuevo repositorio de Git con el comando `git init`.

## Clonar un repositorio Git

Si desea trabajar con un repositorio Git existente, puede clonarlo con el comando `git clone`. La clonación de un repositorio crea una copia local del repositorio remoto.

## Conceptos básicos de Git

Ahora que tiene un repositorio de Git, puede comenzar a trabajar con él.

### Adición de archivos al repositorio

Puede agregar archivos al repositorio de Git con el comando `git add`. Este comando agrega un archivo al área de preparación, que es un área de espera temporal para los cambios.

### Confirmación de cambios

Una vez que haya agregado todos los archivos que desea confirmar, puede enviarlos al repositorio con el comando `git commit`. Este comando guarda sus cambios en el historial de Git.

### Visualización del historial de confirmaciones

Puede ver el historial de confirmaciones con el comando `git log`. Este comando muestra una lista de todas las confirmaciones en la rama actual, comenzando con la confirmación más reciente.

### Comprobación del estado de los archivos

Puede verificar el estado de los archivos en el repositorio de Git con el comando `git status`. Este comando muestra una lista de todos los archivos que se han modificado desde la última confirmación.

### Visualización de diferencias

Puede ver las diferencias entre la versión actual de un archivo y la versión en el repositorio de Git con el comando `git diff`. Este comando es útil para ver qué cambios ha realizado en un archivo antes de confirmarlos.

## Ramas Git

Las ramas de Git se utilizan para crear entornos aislados para el desarrollo. Puedes pensar en una rama como una línea separada de desarrollo.

### Creación de una sucursal

Puedes crear una nueva rama con el comando `git branch`.

### Cambio de sucursales

Puede cambiar entre sucursales con el comando `git checkout`.

### Fusión de ramas

Puede fusionar dos ramas con el comando `git merge`.

## Git remoto

Git remote se usa para administrar repositorios remotos. Un repositorio remoto es un repositorio que no está en su máquina local.

### Agregar un control remoto

Puede agregar un repositorio remoto con el comando `git remote add`.

### Obtener desde un control remoto

Puede obtener cambios de un repositorio remoto con el comando `git fetch`.

### Empujando a un control remoto

Puede enviar cambios a un repositorio remoto con el comando `git push`.

## Etiquetas Git

Las etiquetas de Git se utilizan para marcar puntos específicos en el historial de Git. Las etiquetas se utilizan generalmente para marcar los puntos de liberación.

### Creación de una etiqueta

Puede crear una etiqueta con el comando `git tag`.

### Empujar etiquetas

Puede enviar etiquetas a un repositorio remoto con el comando `git push`.

## Alias Git

Los alias de Git se utilizan para crear accesos directos para los comandos de Git.

Puede crear un alias con el comando `git config`. Por ejemplo, para crear un alias para el comando `git status`, ejecutaría el siguiente comando:

```
git config --global alias.st status
```

Ahora puede usar el comando `git st` para ejecutar el comando `git status`.

## Ganchos Git

Los ganchos de Git son scripts que se ejecutan automáticamente cuando ocurren ciertos eventos en un repositorio de Git. Los ganchos Git son útiles para automatizar tareas.

Los ganchos Git se almacenan en el directorio `.git/hooks`.

## Gitignore

Gitignore se usa para ignorar archivos que Git no debe rastrear. Por ejemplo, es posible que desee ignorar los archivos temporales o los archivos de registro.

Puede crear un archivo `.gitignore` en el directorio raíz de su repositorio Git. El archivo `.gitignore` debe contener una lista de patrones para ignorar.

## Flujo Git

El flujo de Git es un conjunto de convenciones para administrar sucursales en un repositorio de Git. Git flow está diseñado para facilitar el trabajo con ramas.

## GitLab

GitLab es un administrador de repositorios de Git basado en la web. GitLab proporciona una interfaz web para administrar repositorios de Git. GitLab también proporciona funciones para el seguimiento de problemas, la integración continua y la revisión de código.

## GitHub

GitHub es un servicio de alojamiento de repositorio Git basado en la web. GitHub proporciona una interfaz web para administrar repositorios de Git. GitHub también proporciona funciones para el seguimiento de problemas, la integración continua y la revisión de código.

## Bitbucket

Bitbucket es un servicio de alojamiento de repositorio Git basado en la web. Bitbucket proporciona una interfaz web para administrar repositorios de Git. Bitbucket también proporciona funciones para el seguimiento de problemas, la integración continua y la revisión de código.

## Recursos externos

- [Documentación Git](https://git-scm.com/doc)
- [Libro Pro Git](https://git-scm.com/book/en/v2)
- [Aprenda la ramificación de Git] (https://learngitbranching.js.org/)