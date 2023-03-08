---
title: AWS Elastic Beanstalk: implementación y escalado de una aplicación web simple
description: 
published: true
date: 2023-02-09T12:18:12.620Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:18:10.842Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Elastic Beanstalk: Deploying and Scaling a Simple Web Application***English** document is available*](/en/Knowledge-base/Cloud/aws-elastic-beanstalk-deploying-and-scaling-a-simple-web-application)
{.links-list}


# AWS Elastic Beanstalk: implementación y escalado de una aplicación web simple

AWS Elastic Beanstalk es un servicio fácil de usar para implementar y escalar aplicaciones y servicios web desarrollados con marcos de aplicaciones web populares como Java, .NET, PHP, Node.js, Python, Ruby on Rails y Docker en AWS.

Elastic Beanstalk reduce la complejidad de administrar los recursos subyacentes de su aplicación web, como instancias de Amazon EC2, balanceadores de carga y grupos de Auto Scaling. También proporciona una experiencia unificada para monitorear el estado y el rendimiento de su aplicación web.

En este artículo, le mostraremos cómo implementar una aplicación web simple en AWS Elastic Beanstalk. También demostraremos lo fácil que es escalar su aplicación web horizontalmente (agregando más instancias Amazon EC2) y verticalmente (aumentando el tamaño de sus instancias Amazon EC2).

## Requisitos previos

Antes de comenzar, necesitará lo siguiente:

* Una cuenta de AWS. Si no tiene uno, puede crear uno gratis [aquí] (https://aws.amazon.com/getting-started/).
* Una aplicación web que se puede implementar en una instancia de Amazon EC2. Para este artículo, usaremos una aplicación web simple de Node.js.
* Un depósito de Amazon S3 para almacenar el código fuente de su aplicación web.

## Implementación de su aplicación web en AWS Elastic Beanstalk

Para implementar su aplicación web en AWS Elastic Beanstalk, cree un entorno de Elastic Beanstalk y cargue el código fuente de su aplicación en un depósito de Amazon S3. Luego, Elastic Beanstalk creará una instancia de Amazon EC2, cargará su aplicación web en ella y la configurará para atender el tráfico.

### Creación de un entorno de Elastic Beanstalk

Para crear un entorno de Elastic Beanstalk, abra la consola de Elastic Beanstalk y haga clic en "Crear nueva aplicación".

![crear-nueva-aplicación](https://i.imgur.com/lpY7B0m.png)

Introduzca un nombre para su aplicación y haga clic en "Crear".

![ingresar-nombre-para-la-aplicación](https://i.imgur.com/fvqQYxo.png)

En la página siguiente, seleccione la plataforma de servidor web que desea utilizar. Para este artículo, usaremos "Node.js".

![seleccionar-plataforma](https://i.imgur.com/LJNcuAO.png)

En la página siguiente, seleccione el tipo de instancia de Amazon EC2 que desea utilizar. Para este artículo, utilizaremos el tipo de instancia "t2.micro".

![seleccione-ec2-tipo-de-instancia](https://i.imgur.com/VkzM8JZ.png)

En la página siguiente, seleccione el depósito de Amazon S3 que desea utilizar para almacenar el código fuente de su aplicación web.

![select-s3-bucket](https://i.imgur.com/y4FtJjl.png)

Haga clic en "Implementar" para implementar su aplicación web en AWS Elastic Beanstalk.

![implementar-aplicación](https://i.imgur.com/BKW738u.png)

Elastic Beanstalk ahora creará una instancia de Amazon EC2, cargará su aplicación web en ella y la configurará para atender el tráfico.

### Subir el código fuente de su aplicación a Amazon S3

Ahora que ha creado un entorno de Elastic Beanstalk, debe cargar el código fuente de su aplicación web en el depósito de Amazon S3 que seleccionó.

Para hacer esto, abra la consola de Amazon S3 y seleccione el depósito que desea usar. Luego, haga clic en el botón "Subir".

![botón de carga](https://i.imgur.com/TXrQ8oA.png)

En la página siguiente, seleccione los archivos que desea cargar y haga clic en "Cargar".

![seleccionar-archivos-para-cargar](https://i.imgur.com/F3gG0CY.png)

El código fuente de su aplicación web ahora está almacenado en el depósito de Amazon S3.

## Acceso a su aplicación web

Una vez que su aplicación web se haya implementado en AWS Elastic Beanstalk, puede acceder a ella yendo a la URL del entorno.

Para buscar la URL del entorno, abra la consola de Elastic Beanstalk y haga clic en el entorno que creó. Luego, haga clic en la pestaña "Resumen". La URL del entorno se muestra en la parte superior de la página.

![url-entorno](https://i.imgur.com/vzMJO4F.png)

## Escalando su aplicación web

AWS Elastic Beanstalk facilita el escalado de su aplicación web horizontalmente (al agregar más instancias de Amazon EC2) y verticalmente (al aumentar el tamaño de sus instancias de Amazon EC2).

Para escalar su aplicación web horizontalmente, abra la consola de Elastic Beanstalk y haga clic en el entorno que creó. Luego, haga clic en la pestaña "Configuración".

![pestaña de configuración](https://i.imgur.com/J3GfUxz.png)

En la página siguiente, haga clic en la pestaña "Capacidad".

![pestaña de capacidad](https://i.imgur.com/pLJgJw6.png)

En la página siguiente, seleccione la cantidad de instancias de Amazon EC2 que desea usar y haga clic en "Aplicar".

![seleccione-número-de-instancias](https://i.imgur.com/X3XWqlr.png)

Elastic Beanstalk ahora agregará la cantidad deseada de instancias de Amazon EC2 a su entorno.

Para escalar su aplicación web verticalmente, abra la consola de Elastic Beanstalk y haga clic en el entorno que creó. Luego, haga clic en la pestaña "Configuración".

![pestaña de configuración](https://i.imgur.com/J3GfUxz.png)

En la página siguiente, haga clic en la pestaña "Capacidad".

![pestaña de capacidad](https://i.imgur.com/pLJgJw6.png)

En la página siguiente, seleccione el tipo de instancia de Amazon EC2 que desea utilizar y haga clic en "Aplicar".

![select-ec2-instance-type](https://i.imgur.com/IHLv4jO.png)

Elastic Beanstalk ahora reconfigurará su entorno para usar el tipo de instancia de Amazon EC2 deseado.

## Monitoreo de su aplicación web

AWS Elastic Beanstalk brinda una experiencia unificada para monitorear el estado y el rendimiento de su aplicación web.

Para ver las métricas de salud y rendimiento de su aplicación web, abra la consola de Elastic Beanstalk y haga clic en el entorno que creó. Luego, haga clic en la pestaña "Monitoreo".

![pestaña-supervisión](https://i.imgur.com/VxKG0zJ.png)

En la página siguiente, verá un panel con varias métricas sobre su aplicación web, como el recuento de solicitudes, el tiempo de respuesta y la utilización de la CPU.

![Panel de control](https://i.imgur.com/ZDGxK5M.png)

También puede ver los registros de acceso y de error de su aplicación web. Para hacer esto, abra la consola de Elastic Beanstalk y haga clic en el entorno que creó. Luego, haga clic en la pestaña "Registros".

![ficha de registros](https://i.imgur.com/D4Y4lkO.png)

En la página siguiente, verá una lista de los registros de acceso y de error de su aplicación web.

![registros](https://i.imgur.com/rAFwUOI.png)

## Actualización de su aplicación web

Para actualizar su aplicación web, simplemente cargue la versión actualizada del código fuente de su aplicación web en el depósito de Amazon S3 que está utilizando. Elastic Beanstalk detectará automáticamente los cambios e implementará la versión actualizada de su aplicación web.

## Eliminar su aplicación web

Para eliminar su aplicación web, abra la consola de Elastic Beanstalk y haga clic en el entorno que creó. Luego, haga clic en el menú desplegable "Acciones" y seleccione "Eliminar entorno".

![borrar-entorno](https://i.imgur.com/VxJN4jO.png)

En la página siguiente, ingrese un nombre para el entorno que está a punto de eliminar y haga clic en "Eliminar".

![ingresar-nombre-del-entorno](https://i.imgur.com/uvaYG4Y.png)

Elastic Beanstalk ahora eliminará su aplicación web.

## Conclusión

En este artículo, le mostramos cómo implementar una aplicación web simple en AWS Elastic Beanstalk. También hemos demostrado lo fácil que es escalar su aplicación web horizontalmente (agregando más instancias Amazon EC2) y verticalmente (aumentando el tamaño de sus instancias Amazon EC2). Finalmente, también le mostramos cómo monitorear la salud y el rendimiento de su aplicación web.