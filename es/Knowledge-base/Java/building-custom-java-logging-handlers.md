---
title: Creación de controladores de registro de Java personalizados
description: 
published: true
date: 2023-02-07T05:17:59.053Z
tags: 
editor: markdown
dateCreated: 2023-02-07T05:17:57.427Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Custom Java Logging Handlers***English** document is available*](/en/Knowledge-base/Java/building-custom-java-logging-handlers)
{.links-list}


# Creación de controladores de registro de Java personalizados

La plataforma Java proporciona soporte integrado para registrar y registrar eventos en todo el sistema. Además de las muchas opciones disponibles listas para usar, los desarrolladores de Java también pueden crear sus propios controladores de registro personalizados.

Un controlador de registro es un objeto responsable de recibir registros de un registrador y exportarlos a un destino, como un archivo, la consola o un servidor remoto.

En este artículo, veremos cómo crear un controlador de registro personalizado en Java. También exploraremos algunas mejores prácticas para crear y usar controladores de registro.

## Creación de un controlador de registro personalizado

La creación de un controlador de registro personalizado en Java es un proceso de dos pasos. Primero, necesitamos crear una clase que amplíe la clase java.util.logging.Handler. Esta clase definirá el comportamiento de nuestro controlador personalizado.

A continuación, debemos registrar nuestro controlador con java.util.logging.LogManager. Esto se puede hacer mediante programación o utilizando un archivo de configuración.

Echemos un vistazo a un ejemplo de cada enfoque.

### Registro programático

El registro programático es la forma más sencilla de registrar un controlador de registro personalizado. Podemos hacer esto llamando al método LogManager.addHandler(). Este método acepta una instancia de nuestra clase Handler personalizada como parámetro.

Aquí hay un ejemplo:

```java
import java.util.logging.Handler;
import java.util.logging.LogManager;
import java.util.logging.Logger;

public class MyCustomHandler extends Handler {
    // ...
}

public class Main {
    public static void main(String[] args) {
        // create an instance of our custom handler
        Handler handler = new MyCustomHandler();
        
        // get the root logger
        Logger logger = LogManager.getLogManager().getLogger("");
        
        // add our handler to the root logger
        logger.addHandler(handler);
    }
}
```

En el ejemplo anterior, primero creamos una instancia de nuestra clase Handler personalizada. A continuación, obtenemos el registrador raíz del LogManager. Finalmente, agregamos nuestro controlador al registrador raíz.

### Registro del archivo de configuración

El registro del archivo de configuración es un poco más complejo que el registro programático, pero ofrece más flexibilidad.

Con el registro del archivo de configuración, necesitamos crear un archivo llamado "logging.properties" en el directorio "conf" de nuestra aplicación Java. Este archivo contiene varias propiedades que configuran el sistema de registro de Java.

Este es un ejemplo de un archivo logging.properties:

```
# default logging level
.level=INFO

# default handler
handlers=java.util.logging.ConsoleHandler

# custom handler
com.example.MyCustomHandler.level=ALL
com.example.MyCustomHandler.formatter=java.util.logging.SimpleFormatter
com.example.MyCustomHandler.encoding=UTF-8
```

En el ejemplo anterior, hemos definido una serie de propiedades para nuestro controlador personalizado. La primera propiedad, "nivel", especifica el nivel de registro de nuestro controlador. La segunda propiedad, "formateador", especifica el formateador que utilizará nuestro controlador. La tercera propiedad, "codificación", especifica la codificación de caracteres que utilizará nuestro controlador.

## Prácticas recomendadas para crear controladores de registro personalizados

Ahora que hemos visto cómo crear un controlador de registro personalizado en Java, echemos un vistazo a algunas de las mejores prácticas para crear y usar controladores de registro.

### Mantenlo simple

Al crear un controlador de registro personalizado, es importante mantener el diseño simple. Una buena regla general es anular solo los métodos que son absolutamente necesarios.

Por ejemplo, la clase java.util.logging.Handler define una serie de métodos para gestionar los registros. Sin embargo, solo necesitamos anular el método de publicación(). Los otros métodos se pueden dejar como están.

### Usar controladores existentes como punto de partida

Al crear un controlador de registro personalizado, suele ser útil utilizar un controlador existente como punto de partida. Por ejemplo, la clase java.util.logging.ConsoleHandler es un controlador simple que escribe registros en la consola.

Si estamos creando un controlador que escribe registros en un archivo, podemos usar la clase java.util.logging.FileHandler como punto de partida. Esta clase define todos los métodos necesarios para escribir registros en un archivo.

### No bloquee el hilo del registrador

Al crear un controlador de registro personalizado, es importante evitar bloquear el hilo del registrador. Un controlador de bloqueo puede hacer que el registrador deje de procesar los registros.

Una forma de evitar bloquear el subproceso del registrador es utilizar un subproceso separado para exportar los registros. Por ejemplo, la clase java.util.logging.AsyncHandler utiliza un subproceso independiente para exportar registros.

Otra forma de evitar bloquear el hilo del registrador es usar una cola. La clase java.util.logging.QueueHandler utiliza una cola para almacenar registros. A continuación, los registros se exportan mediante un subproceso independiente.

### Usar un formateador

Al crear un controlador de registro personalizado, es importante utilizar un formateador. Un formateador es un objeto que se encarga de convertir un registro en una cadena.

La clase java.util.logging.Handler define un método setFormatter() que se puede usar para configurar el formateador para un controlador. De forma predeterminada, se llama a este método cuando se crea un controlador.

Si usamos un formateador personalizado, debemos asegurarnos de que el formateador sea seguro para subprocesos. Esto se debe a que varios subprocesos pueden llamar al formateador.

Una forma de garantizar que un formateador sea seguro para subprocesos es utilizar la clase java.util.logging.ThreadLocalFormatter. Esta clase define un formateador que es específico para el subproceso actual.

Otra forma de garantizar que un formateador sea seguro para subprocesos es utilizar la clase java.util.logging.SynchronizedFormatter. Esta clase envuelve un formateador existente y sincroniza todos los métodos del formateador.

### Usar un filtro

Al crear un controlador de registro personalizado, a menudo es útil usar un filtro. Un filtro es un objeto que es responsable de determinar qué entradas de registro debe exportar un controlador.

La clase java.util.logging.Handler define un método setFilter() que se puede usar para establecer el filtro para un controlador. De forma predeterminada, se llama a este método cuando se crea un controlador.

Si usamos un filtro personalizado, debemos asegurarnos de que el filtro sea seguro para subprocesos. Esto se debe a que varios subprocesos pueden llamar al filtro.

Una forma de garantizar que un filtro sea seguro para subprocesos es utilizar la clase java.util.logging.SynchronizedFilter. Esta clase envuelve un filtro existente y sincroniza todos los métodos del filtro.

Otra forma de garantizar que un filtro sea seguro para subprocesos es utilizar la clase java.util.logging.ThreadLocalFilter. Esta clase define un filtro que es específico para el subproceso actual.

### Usa un candado

Al crear un controlador de registro personalizado, a menudo es útil usar un candado. Un bloqueo es un objeto que se utiliza para sincronizar el acceso a un recurso.

La clase java.util.logging.Handler define un método setLock() que se puede utilizar para establecer el bloqueo de un controlador. De forma predeterminada, se llama a este método cuando se crea un controlador.

Si usamos un bloqueo personalizado, debemos asegurarnos de que el bloqueo sea seguro para subprocesos. Esto se debe a que varios subprocesos pueden acceder al bloqueo.

Una forma de garantizar que un bloqueo sea seguro para subprocesos es utilizar la clase java.util.concurrent.locks.ReentrantLock. Esta clase define un bloqueo que pueden utilizar varios subprocesos.

Otra forma de garantizar que un bloqueo sea seguro para subprocesos es utilizar la clase java.util.concurrent.locks.Lock. Esta clase envuelve un bloqueo existente y sincroniza todos los métodos del bloqueo.

## Conclusión

En este artículo, hemos visto cómo crear un controlador de registro personalizado en Java. También hemos visto cómo registrar nuestro controlador con java.util.logging.LogManager. Finalmente, analizamos algunas de las mejores prácticas para crear y usar controladores de registro.