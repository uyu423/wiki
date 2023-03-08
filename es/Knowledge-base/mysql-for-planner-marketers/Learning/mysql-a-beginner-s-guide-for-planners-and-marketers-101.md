---
title: MySQL Una guía para principiantes para planificadores y especialistas en marketing: 101
description: 
published: true
date: 2023-02-06T16:34:09.427Z
tags: 
editor: markdown
dateCreated: 2023-02-06T16:34:07.580Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL A Beginner's Guide for Planners and Marketers: 101***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-a-beginner-s-guide-for-planners-and-marketers-101)
{.links-list}


MySQL es un poderoso sistema de administración de bases de datos utilizado por aplicaciones web para almacenar datos. Es uno de los sistemas de base de datos más populares en uso hoy en día.

MySQL es un sistema de gestión de bases de datos relacionales (RDBMS). Esto significa que almacena datos en tablas que están relacionadas entre sí. Por ejemplo, una tabla de datos de clientes podría estar relacionada con una tabla de datos de pedidos.

MySQL es un software gratuito y de código abierto. Esto significa que está disponible para que cualquiera lo use y modifique.

MySQL es una opción popular para aplicaciones web porque es rápido, confiable y fácil de usar.

En esta guía, aprenderemos los conceptos básicos de MySQL. Cubriremos los siguientes temas:

- Instalación de MySQL
- Creación de una base de datos
- Creación de tablas
- Inserción de datos
- Consulta de datos
- Copia de seguridad y restaurar

## Instalación de MySQL

MySQL se puede instalar en Windows, macOS y Linux. También se puede instalar en un servidor que ejecute otro sistema operativo, como FreeBSD.

La forma más sencilla de instalar MySQL en Windows es utilizar el instalador de MySQL. Esto instalará todos los componentes que necesitamos, incluido MySQL Server, MySQL Workbench y MySQL Notifier.

Descargue el instalador de MySQL desde el sitio web de MySQL:

https://dev.mysql.com/downloads/installer/

Ejecute el instalador y siga las indicaciones. Cuando se le solicite, elija las siguientes opciones:

- Instalar servidor MySQL
- Configure el servidor MySQL ahora

Se iniciará el asistente de configuración. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija una contraseña para el usuario root de MySQL. Este es el usuario que tiene acceso total a todas las bases de datos MySQL.

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows
- Incluir Bin Directory en Windows PATH

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP
- Habilitar modo estricto

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija las siguientes opciones:

- Instalar como servicio de Windows: Sí
- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Número de puerto: 3306
- Habilitar redes TCP/IP: Sí
- Habilitar modo estricto: Sí

En la página siguiente, elija las siguientes opciones:

- Conjunto de caracteres predeterminado: utf8
- Instalar MySQL Test Suite: Sí

En la página siguiente, elija las siguientes opciones:

- Notificador MySQL: No Requerido
- Banco de trabajo MySQL: no requerido

En la página siguiente, elija las siguientes opciones:

- Crear una cuenta anónima: No
- Habilitar validación de contraseña estricta: No

En la página siguiente, elija las siguientes opciones:

- Ejecutar MySQL Server como un servicio de Windows: Sí
- Inicie el servidor MySQL automáticamente: Sí

En la página siguiente, elija las siguientes opciones:

- Incluir Bin Directory en Windows PATH: Sí

En la página siguiente, elija las siguientes opciones:

- Configurar MySQL Server ahora: Sí

Se iniciará el asistente de configuración del servidor MySQL. En la primera página, elija las siguientes opciones:

- Tipo de servidor: Máquina de desarrollo
- Uso de la base de datos: base de datos multifuncional
- Soporte de base de datos transaccional: InnoDB
- Soporte de base de datos no transaccional: MyISAM

En la página siguiente, elija el