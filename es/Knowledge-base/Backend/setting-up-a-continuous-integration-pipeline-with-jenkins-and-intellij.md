---
title: Configuración de una canalización de integración continua con Jenkins e IntelliJ
description: 
published: true
date: 2023-02-13T13:18:15.332Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:18:08.216Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Setting up a Continuous Integration Pipeline with Jenkins and IntelliJ***English** document is available*](/en/Knowledge-base/Backend/setting-up-a-continuous-integration-pipeline-with-jenkins-and-intellij)
{.links-list}


# Configuración de una canalización de integración continua con Jenkins e IntelliJ

## Introducción

La integración continua (CI) es una práctica de desarrollo que requiere que los desarrolladores integren código en un repositorio compartido varias veces al día. Luego, cada registro se verifica mediante una compilación automatizada, lo que permite a los equipos detectar problemas con anticipación.

Configurar una tubería de CI puede ser una tarea abrumadora, pero con las herramientas adecuadas puede ser relativamente simple. En este artículo, le mostraremos cómo configurar una canalización de CI con Jenkins e IntelliJ.

## Que necesitarás

- Una cuenta de GitHub
- Un servidor Jenkins
- IDEA IntelliJ

## Paso 1: crea un repositorio de GitHub

El primer paso es crear un repositorio de GitHub para su proyecto. Para hacer esto, dirígete a GitHub y crea un nuevo repositorio.

![Crear un nuevo repositorio de GitHub](https://i.imgur.com/EuU8GtO.png)

Asigne un nombre a su repositorio y haga clic en "Crear repositorio".

![Nombra tu repositorio](https://i.imgur.com/VNcuCY5.png)

## Paso 2: Crear un trabajo de Jenkins

A continuación, necesitamos crear un trabajo de Jenkins. Un trabajo de Jenkins es una tarea que Jenkins puede ejecutar. En nuestro caso, el trabajo de Jenkins verificará nuestro código de GitHub, lo compilará y ejecutará nuestras pruebas.

Para crear un trabajo de Jenkins, diríjase a su servidor de Jenkins y haga clic en "Nuevo trabajo".

![Nuevo trabajo de Jenkins](https://i.imgur.com/pLJnV1N.png)

Asigne un nombre a su trabajo y seleccione "Proyecto de estilo libre".

![ Nombre del trabajo de Jenkins](https://i.imgur.com/lGZm4z3.png)

Haga clic en Aceptar".

En la página siguiente, desplácese hacia abajo hasta la sección "Administración de código fuente" y seleccione "Git".

![Administración del código fuente de Jenkins](https://i.imgur.com/Lg4U4jf.png)

En el campo "URL del repositorio", ingrese la URL de su repositorio de GitHub.

![URL del repositorio de Jenkins](https://i.imgur.com/VkzM0cw.png)

Desplácese hacia abajo hasta la sección "Construir" y haga clic en "Agregar paso de compilación". Seleccione "Ejecutar shell".

![Sección de compilación de Jenkins](https://i.imgur.com/KJ3fZUO.png)

En el campo "Comando", ingrese el siguiente comando:

```
mvn clean install
```

Este comando limpiará nuestro proyecto, instalará las dependencias y ejecutará nuestras pruebas.

Desplácese hacia abajo hasta la sección "Acciones posteriores a la compilación" y haga clic en "Agregar acción posterior a la compilación". Seleccione "Publicar informe de resultados de prueba JUnit".

![Acciones posteriores a la compilación de Jenkins](https://i.imgur.com/NDYaTGi.png)

En el campo "XML de informe de prueba", ingrese lo siguiente:

```
**/target/surefire-reports/*.xml
```

Esto le indicará a Jenkins que publique los resultados de nuestras pruebas.

Clic en Guardar".

## Paso 3: configurar IntelliJ

Ahora que tenemos nuestro trabajo de Jenkins configurado, necesitamos configurar nuestro IDE. En esta sección, le mostraremos cómo configurar IntelliJ para activar una compilación en nuestro servidor Jenkins cuando hacemos cambios en nuestro código.

Abra IntelliJ y navegue hasta el menú "Archivo". Seleccione "Configuración".

![Configuración de IntelliJ](https://i.imgur.com/mEUDKjK.png)

En la ventana "Configuración", navegue hasta "Construir, Ejecución, Implementación" > "Integración continua". Seleccione "Jenkins".

![IntelliJ Jenkins](https://i.imgur.com/VkzM0cw.png)

En el campo "URL de Jenkins", ingrese la URL de su servidor Jenkins.

![URL de IntelliJ Jenkins](https://i.imgur.com/dc9gKbD.png)

En el campo "Nombre del proyecto", ingrese el nombre de su trabajo de Jenkins.

![Nombre del proyecto IntelliJ](https://i.imgur.com/P0zM0cw.png)

Haga clic en Aceptar".

## Paso 4: activa una compilación

Ahora que nuestro trabajo de Jenkins está configurado y nuestro IDE está configurado, estamos listos para activar una compilación. Para hacer esto, realice un cambio en su código y envíelo a GitHub.

![Enviar IntelliJ a GitHub](https://i.imgur.com/VkzM0cw.png)

Una vez que envíe su código a GitHub, Jenkins detectará automáticamente el cambio, verificará el código, lo compilará y ejecutará las pruebas.

![Compilación Jenkins](https://i.imgur.com/u4JnV1N.png)

Puede ver los resultados de la compilación haciendo clic en el enlace "crear" en la sección "Historial de compilación".

![Historial de compilación de Jenkins](https://i.imgur.com/ VkzM0cw.png)

## Conclusión

En este artículo, le mostramos cómo configurar una canalización de CI con Jenkins e IntelliJ. Si bien se trata de una canalización simple, se puede ampliar fácilmente para incluir pasos adicionales, como la implementación en un entorno de ensayo o de producción.