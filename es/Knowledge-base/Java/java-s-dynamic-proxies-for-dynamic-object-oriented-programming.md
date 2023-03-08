---
title: Proxies dinámicos de Java para programación dinámica orientada a objetos
description: 
published: true
date: 2023-02-03T06:23:35.263Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:23:33.658Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's Dynamic Proxies for Dynamic Object Oriented Programming***English** document is available*](/en/Knowledge-base/Java/java-s-dynamic-proxies-for-dynamic-object-oriented-programming)
{.links-list}



# Proxies dinámicos de Java para programación dinámica orientada a objetos

Los proxies dinámicos de Java permiten una forma segura de tipos y orientada a objetos para crear código dinámico. En este artículo, exploraremos cómo usar proxies dinámicos para crear código dinámico y cómo se pueden usar en aplicaciones prácticas.

## ¿Qué son los proxies dinámicos?

Un proxy dinámico es una clase que implementa una lista de interfaces especificadas en tiempo de ejecución. Cuando se invoca un método en una instancia de proxy dinámico, la invocación del método se reenvía al método de invocación() de la clase Proxy, que envía la llamada al controlador de método apropiado.

Se puede usar un proxy dinámico para crear un "envoltorio" alrededor de un objeto, que se puede usar para agregar funcionalidad al objeto sin modificar el código original. Por ejemplo, se podría usar un proxy dinámico para agregar registros a todas las llamadas a métodos en un objeto, o para agregar comprobaciones de seguridad antes de permitir que se invoque un método.

## Creación de un proxy dinámico

Crear un proxy dinámico es relativamente simple. Primero, debe crear una instancia de la clase Proxy, pasando el ClassLoader para la clase que desea representar y una matriz de interfaces que el proxy debería implementar. Por ejemplo:

```java
ClassLoader classLoader = MyObject.class.getClassLoader();
Class[] interfaces = new Class[] { MyObject.class };

MyObject myObject = (MyObject) Proxy.newProxyInstance(classLoader, interfaces, new MyObjectInvocationHandler(myObject));
```

En el ejemplo anterior, usamos la clase Proxy para crear un proxy dinámico para la clase MyObject. La clase MyObject debe ser cargable por el ClassLoader dado y debe implementar la interfaz MyObject. El tercer argumento del método Proxy.newProxyInstance() es una instancia de InvocationHandler, que es responsable de manejar las llamadas a métodos en el proxy.

En el ejemplo anterior, creamos un InvocationHandler simple que simplemente reenvía llamadas de método al objeto original. Sin embargo, podría agregar fácilmente su propia lógica al InvocationHandler, como registrar llamadas a métodos o agregar comprobaciones de seguridad.

## Uso de un proxy dinámico

Una vez que haya creado un proxy dinámico, puede usarlo como cualquier otro objeto. Por ejemplo, si tiene un proxy dinámico para la clase MyObject, puede invocar métodos en el proxy como lo haría en el objeto original:

```java
myObject.doSomething();
```

## ¿Por qué usar proxies dinámicos?

Los proxies dinámicos son una herramienta poderosa para crear código dinámico. Se pueden usar para agregar funcionalidad a un objeto sin modificar el código original, lo que puede ser muy útil en situaciones en las que no tiene acceso al código fuente.

Los proxies dinámicos también se pueden usar para crear objetos de "envoltura" que se pueden usar para agregar funcionalidad a un objeto sin cambiar la interfaz del objeto. Por ejemplo, podría usar un proxy dinámico para crear un contenedor alrededor de un objeto que agregue registro a todas las llamadas a métodos en el objeto, sin cambiar la interfaz del objeto.

## Cuándo usar proxies dinámicos

Los proxies dinámicos pueden ser muy útiles en situaciones en las que necesita agregar funcionalidad a un objeto sin modificar el código original. También se pueden usar para crear objetos de "envoltura" que se pueden usar para agregar funcionalidad a un objeto sin cambiar la interfaz del objeto.

## Cuándo no usar proxies dinámicos

Los proxies dinámicos no deben usarse en situaciones en las que el rendimiento es crítico, ya que agregan una capa de direccionamiento indirecto que puede afectar el rendimiento. Tampoco deben usarse en situaciones en las que el objeto subyacente debe pasarse a un método nativo, ya que la JVM no admite de forma nativa la clase Proxy.

## Conclusión

Los proxies dinámicos son una herramienta poderosa para crear código dinámico. Se pueden usar para agregar funcionalidad a un objeto sin modificar el código original, lo que puede ser muy útil en situaciones en las que no tiene acceso al código fuente. Los proxies dinámicos también se pueden usar para crear objetos de "envoltura" que se pueden usar para agregar funcionalidad a un objeto sin cambiar la interfaz del objeto.