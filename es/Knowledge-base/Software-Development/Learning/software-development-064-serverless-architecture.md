---
title: Desarrollo de software 064: arquitectura sin servidor
description: 
published: true
date: 2023-02-16T17:55:54.773Z
tags: 
editor: markdown
dateCreated: 2023-02-16T17:55:52.727Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 064: Serverless Architecture***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-064-serverless-architecture)
{.links-list}


# Desarrollo de software 064: Arquitectura sin servidor

El término "sin servidor" ha ganado mucha popularidad últimamente, pero ¿qué significa realmente?

En una aplicación web tradicional, el código de la aplicación se implementa en un servidor y el servidor es responsable de manejar las solicitudes de los clientes. Sin embargo, en una aplicación sin servidor, el código de la aplicación se implementa "en la nube" y se ejecuta en respuesta a eventos.

Hay muchos beneficios al usar una arquitectura sin servidor, que incluyen:

- Gastos generales operativos reducidos: dado que no hay necesidad de administrar servidores, las aplicaciones sin servidor son mucho más fáciles de mantener.

- Escalabilidad: dado que el código de la aplicación se ejecuta en respuesta a eventos, puede escalar automáticamente para satisfacer la demanda.

- Rentable: dado que no es necesario aprovisionar ni mantener servidores, las aplicaciones sin servidor pueden ser muy rentables.

En esta publicación, veremos qué es una arquitectura sin servidor y cómo comenzar a desarrollar aplicaciones sin servidor.

## ¿Qué es una arquitectura sin servidor?

En una aplicación web tradicional, el código de la aplicación se implementa en un servidor y el servidor es responsable de manejar las solicitudes de los clientes. Sin embargo, en una aplicación sin servidor, el código de la aplicación se implementa "en la nube" y se ejecuta en respuesta a eventos.

Hay muchos beneficios al usar una arquitectura sin servidor, que incluyen:

- Gastos generales operativos reducidos: dado que no hay necesidad de administrar servidores, las aplicaciones sin servidor son mucho más fáciles de mantener.

- Escalabilidad: dado que el código de la aplicación se ejecuta en respuesta a eventos, puede escalar automáticamente para satisfacer la demanda.

- Rentable: dado que no es necesario aprovisionar ni mantener servidores, las aplicaciones sin servidor pueden ser muy rentables.

## Primeros pasos con Serverless

Hay muchas plataformas diferentes que le permiten desarrollar aplicaciones sin servidor, pero en esta publicación nos centraremos en AWS Lambda.

AWS Lambda es una plataforma que le permite ejecutar código en la nube sin tener que aprovisionar ni administrar servidores. Las funciones de Lambda se ejecutan en respuesta a eventos, como una solicitud HTTP o la carga de un archivo.

Para comenzar a desarrollar funciones de Lambda, primero debe crear una cuenta de AWS. Una vez que haya hecho esto, puede crear una función Lambda utilizando la consola de AWS.

Al crear una función Lambda, deberá especificar un nombre y una descripción, así como el código que ejecutará la función. Las funciones de Lambda se pueden escribir en cualquiera de los lenguajes admitidos, incluidos Node.js, Python y Java.

Una vez que haya creado su función Lambda, puede probarla invocándola con un evento. Por ejemplo, si usa Node.js, puede invocar su función con el siguiente evento:

```javascript
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

Si su función está escrita en Python, puede invocarla con el siguiente evento:

```python
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

Una vez que haya probado su función de Lambda, puede implementarla creando una función de AWS Lambda.

## Conclusión

En esta publicación, analizamos qué es una arquitectura sin servidor y cómo comenzar a desarrollar aplicaciones sin servidor. Las aplicaciones sin servidor pueden ser una excelente manera de reducir los gastos generales y los costos operativos, y pueden escalar automáticamente para satisfacer la demanda.

Si está interesado en obtener más información sobre las arquitecturas sin servidor, consulte los siguientes recursos:

- [¿Qué es Serverless?](https://serverless.com/learn/what-is-serverless/)

- [Introducción a Serverless en AWS](https://aws.amazon.com/getting-started/projects/build-serverless-applications/)

- [Arquitecturas sin servidor](https://martinfowler.com/articles/serverless.html)