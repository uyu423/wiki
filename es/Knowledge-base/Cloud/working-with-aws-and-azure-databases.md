---
title: Trabajar con bases de datos de AWS y Azure
description: 
published: true
date: 2023-02-17T04:18:31.059Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:17:31.045Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with AWS and Azure Databases***English** document is available*](/en/Knowledge-base/Cloud/working-with-aws-and-azure-databases)
{.links-list}


# Trabajar con bases de datos AWS y Azure

Esta guía proporciona una descripción general del trabajo con bases de datos en la nube mediante Amazon Web Services (AWS) y Microsoft Azure. Cubre las diferencias clave entre las dos plataformas, ofrece consejos sobre el diseño de bases de datos basadas en la nube y proporciona información práctica y soluciones del mundo real para el desarrollo de TI.

## AWS frente a bases de datos de Azure

Hay varias diferencias clave entre las bases de datos de AWS y Azure que es importante tener en cuenta al diseñar una solución de base de datos basada en la nube.

### Costo

AWS ofrece un modelo de precios de pago por uso, sin costos iniciales, mientras que Azure cobra una tarifa mensual.

### Almacenamiento

AWS ofrece almacenamiento ilimitado para todos los tipos de bases de datos, mientras que Azure limita el almacenamiento a 10 GB para bases de datos SQL y 50 GB para bases de datos NoSQL.

### Copia de seguridad y recuperación

AWS ofrece copia de seguridad y recuperación automáticas para todos los tipos de bases de datos, mientras que Azure solo ofrece esto para bases de datos SQL.

### Escalabilidad

AWS ofrece escalabilidad horizontal para todos los tipos de bases de datos, mientras que Azure solo ofrece escalabilidad vertical para bases de datos SQL.

## Consejos para diseñar bases de datos basadas en la nube

Hay varios factores importantes a considerar al diseñar una base de datos basada en la nube.

### Almacenamiento

Considere los requisitos de almacenamiento de la base de datos y si es necesario un almacenamiento ilimitado. De lo contrario, Azure puede ser una opción más rentable.

### Copia de seguridad y recuperación

Si la copia de seguridad y la recuperación automáticas no son un requisito, Azure puede ser una opción más rentable.

### Escalabilidad

Tenga en cuenta los requisitos de escalabilidad de la base de datos. Si la escalabilidad horizontal no es un requisito, Azure puede ser una opción más rentable.

## Información práctica y soluciones del mundo real

Las siguientes secciones brindan información práctica y soluciones del mundo real para trabajar con bases de datos en la nube.

### Creando una base de datos en AWS

Para crear una base de datos en AWS, utilice la consola de Amazon RDS.

1. En la consola de Amazon RDS, seleccione **Crear base de datos**.

2. Seleccione el motor de base de datos que desea utilizar.

3. Especifique los detalles de configuración de la base de datos.

4. Seleccione el tamaño de la instancia.

5. Seleccione el tipo de almacenamiento.

6. Configure los ajustes de seguridad.

7. Revise la configuración de la base de datos.

8. Seleccione **Crear base de datos**.

### Crear una base de datos en Azure

Para crear una base de datos en Azure, use Azure Portal.

1. En Azure Portal, seleccione **Crear un recurso**.

2. Seleccione **Bases de datos**.

3. Seleccione el motor de base de datos que desea utilizar.

4. Especifique los detalles de configuración de la base de datos.

5. Seleccione el tamaño de la instancia.

6. Seleccione el tipo de almacenamiento.

7. Configure los ajustes de seguridad.

8. Revise la configuración de la base de datos.

9. Seleccione **Crear**.

### Conexión a una base de datos en AWS

Para conectarse a una base de datos en AWS, utilice la consola de Amazon RDS.

1. En la consola de Amazon RDS, seleccione la base de datos a la que desea conectarse.

2. Seleccione la pestaña **Conexiones**.

3. Seleccione **Crear nueva conexión**.

4. Especifique los detalles de la conexión.

5. Seleccione **Crear conexión**.

6. Copie la cadena de conexión.

7. Pegue la cadena de conexión en el código de su aplicación.

### Conexión a una base de datos en Azure

Para conectarse a una base de datos en Azure, use Azure Portal.

1. En Azure Portal, seleccione la base de datos a la que desea conectarse.

2. Seleccione la pestaña **Resumen**.

3. Seleccione **Mostrar cadena de conexión**.

4. Copie la cadena de conexión.

5. Pegue la cadena de conexión en el código de su aplicación.

## Recursos externos

Para obtener más información sobre cómo trabajar con bases de datos de AWS y Azure, consulte los siguientes recursos:

- [Servicios de base de datos de AWS](https://aws.amazon.com/databases/)
- [Servicios de base de datos de Azure](https://azure.microsoft.com/en-us/services/database/)
- [Diseño de bases de datos relacionales basadas en la nube](https://aws.amazon.com/articles/17286/designing-cloud-based-relational-databases/)
- [Diseño de bases de datos NoSQL basadas en la nube](https://aws.amazon.com/articles/16989/designing-cloud-based-nosql-databases/)