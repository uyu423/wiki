---
title: Creación de cargadores de clases personalizados en Java
description: 
published: true
date: 2023-02-12T17:17:48.387Z
tags: 
editor: markdown
dateCreated: 2023-02-12T17:17:41.618Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Custom Class Loaders in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-class-loaders-in-java)
{.links-list}


# Creación de cargadores de clases personalizados en Java

Al desarrollar aplicaciones Java, es posible que deba crear su propio cargador de clases personalizado. Este suele ser el caso cuando desea cargar clases desde una ubicación que no sea la vía de acceso de clases predeterminada, o cuando desea modificar la forma en que se cargan las clases.

En este artículo, veremos cómo crear un cargador de clases personalizado en Java. También veremos algunos de los casos de uso comunes para los cargadores de clases personalizados.

## ¿Qué es un cargador de clases?

Antes de sumergirnos en cómo crear un cargador de clases personalizado, primero demos un paso atrás y entendamos qué es un cargador de clases.

Un cargador de clases es una pieza de software que se encarga de cargar clases en una aplicación Java. Cuando se inicia una aplicación Java, la máquina virtual Java (JVM) carga un cargador de clases. Este cargador de clases es responsable de cargar las clases de la aplicación.

La JVM viene con un cargador de clases predeterminado, llamado cargador de clases de arranque. Este cargador de clases es responsable de cargar las clases principales de Java, como `java.lang.String` y `java.util.ArrayList`.

Además del cargador de clases de arranque, la JVM viene con otros dos cargadores de clases: el cargador de clases del sistema y el cargador de clases de extensión.

El cargador de clases del sistema es responsable de cargar las clases en el classpath de la aplicación. El classpath es una lista de ubicaciones en las que la JVM debe buscar clases. Por defecto, el classpath incluye los directorios `jre/lib/` y `jre/class/`.

El cargador de clases de extensión es responsable de cargar las clases en el directorio `extensiones/`. El directorio `extensions/` es donde los desarrolladores pueden colocar los archivos JAR que quieren que estén disponibles para todas las aplicaciones del sistema.

## ¿Por qué necesitaría un cargador de clases personalizado?

Ahora que hemos revisado qué es un cargador de clases, echemos un vistazo a algunas de las razones por las que podría necesitar crear un cargador de clases personalizado.

### Cargando clases desde una ubicación diferente

Una razón común para crear un cargador de clases personalizado es cargar clases desde una ubicación distinta a la ruta de clases predeterminada.

Por ejemplo, supongamos que tiene un directorio en su sistema de archivos que contiene algunas clases personalizadas que desea cargar en su aplicación. Podría agregar este directorio a su classpath, pero entonces su aplicación solo podría cargar clases desde ese directorio.

Si desea que su aplicación pueda cargar clases desde varios directorios, deberá crear un cargador de clases personalizado. Este cargador de clases personalizado puede buscar clases en varios directorios, no solo en el classpath.

### Modificar la forma en que se cargan las clases

Otra razón común para crear un cargador de clases personalizado es modificar la forma en que se cargan las clases.

Por ejemplo, supongamos que tiene un archivo JAR que contiene algunas clases que desea cargar en su aplicación. Sin embargo, no desea que el cargador de clases del sistema cargue estas clases. En su lugar, desea utilizar un cargador de clases personalizado que cargará estas clases en un espacio de nombres separado.

Este es solo un ejemplo de cómo podría querer modificar la forma en que se cargan las clases. Hay muchas otras posibilidades.

## Creación de un cargador de clases personalizado

Ahora que hemos visto algunas de las razones por las que podría necesitar crear un cargador de clases personalizado, echemos un vistazo a cómo crear uno.

Crear un cargador de clases personalizado es relativamente simple. Solo necesita crear una clase que amplíe `java.lang.ClassLoader`. Esta clase debe anular el método `loadClass()`.

Aquí hay un ejemplo simple:

```java
public class MyClassLoader extends ClassLoader {
 
    @Override
    public Class<?> loadClass(String name) throws ClassNotFoundException {
        // Load the class from the filesystem
        // ...
        // Return the loaded class
        return null;
    }
}
```

En este ejemplo, hemos creado un cargador de clases personalizado que carga clases desde el sistema de archivos. Este cargador de clases en realidad no carga ninguna clase, pero proporciona un esqueleto que puede usar para crear su propio cargador de clases personalizado.

## Uso de un cargador de clases personalizado

Una vez que haya creado un cargador de clases personalizado, debe indicarle a la JVM que lo use. Puede hacer esto configurando la propiedad del sistema `java.class.path`.

Por ejemplo, supongamos que tiene un cargador de clases personalizado que carga clases desde el directorio `/path/to/classes`. Puede decirle a la JVM que use este cargador de clases configurando la propiedad del sistema `java.class.path` en `/path/to/classes`.

Puede configurar la propiedad del sistema `java.class.path` en la línea de comando cuando inicia su aplicación Java:

```
java -Djava.class.path=/path/to/classes MyApplication
```

Alternativamente, puede establecer la propiedad del sistema mediante programación:

```java
System.setProperty("java.class.path", "/path/to/classes");
```

Una vez que haya configurado la propiedad del sistema `java.class.path`, la JVM utilizará su cargador de clases personalizado para cargar las clases.

## Conclusión

En este artículo, hemos visto cómo crear un cargador de clases personalizado en Java. También hemos visto algunos de los casos de uso comunes para cargadores de clases personalizados.