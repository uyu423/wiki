---
title: 021: Procesamiento de anotaciones en Kotlin: generación de código en tiempo de compilación
description: 
published: true
date: 2023-02-01T16:44:21.483Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:44:19.783Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [021: Annotation Processing in Kotlin: Generating Code at Compile Time***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/021-annotation-processing-in-kotlin-generating-code-at-compile-time)
{.links-list}


# 021: Procesamiento de anotaciones en Kotlin: generación de código en tiempo de compilación

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la JVM. Es totalmente interoperable con Java y se puede utilizar para desarrollar aplicaciones de Android. Kotlin también tiene un excelente soporte para el procesamiento de anotaciones.

El procesamiento de anotaciones es una forma de generar código en tiempo de compilación. A menudo se usa para crear código que no se puede expresar fácilmente en el código fuente del lenguaje de programación. Por ejemplo, el procesamiento de anotaciones se puede usar para generar código para el enlace de datos, para crear paquetes de Android o para generar código para Dagger 2.

En este artículo, veremos cómo usar el procesamiento de anotaciones en Kotlin para generar código para una biblioteca de enlace de datos simple. También veremos cómo usar el complemento kotlin-apt para realizar el procesamiento de anotaciones.

## ¿Qué es el procesamiento de anotaciones?

El procesamiento de anotaciones es una forma de generar código en tiempo de compilación. Los procesadores de anotaciones son programas que leen el código fuente de un programa y generan código basado en las anotaciones presentes en el código fuente.

Las anotaciones son una forma de agregar metadatos a un programa. En Kotlin, las anotaciones se agregan a un programa usando el símbolo `@`. Por ejemplo, la anotación `@Override` se puede usar para anotar un método que anula un método en una superclase.

 Las anotaciones también se pueden usar para agregar metadatos a una clase. En Kotlin, una clase se puede anotar con la anotación `@Deprecated` para indicar que la clase está en desuso y no se debe usar.

Las anotaciones también se pueden usar para agregar metadatos a un paquete. En Kotlin, un paquete se puede anotar con la anotación `@file:JvmName` para indicar que el paquete debe compilarse en una clase Java con el nombre dado.

Las anotaciones también se pueden usar para agregar metadatos a un archivo. En Kotlin, un archivo se puede anotar con la anotación `@file:Suppress("unused")` para indicar que el compilador no debe generar advertencias para variables no utilizadas en el archivo.

## Cómo usar el procesamiento de anotaciones en Kotlin

El procesamiento de anotaciones es una forma de generar código en tiempo de compilación. En Kotlin, el procesamiento de anotaciones se realiza mediante el complemento kotlin-apt. El complemento kotlin-apt es un complemento del compilador de Kotlin que agrega soporte para el procesamiento de anotaciones.

Para usar el complemento kotlin-apt, debe agregar lo siguiente a su archivo `build.gradle`:

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath "com.google.auto.service:auto-service:1.0-rc4"
    }
}

apply plugin: 'kotlin-apt'

dependencies {
    apt "com.google.auto.service:auto-service:1.0-rc4"
}
```

El complemento kotlin-apt agrega una configuración `apt` al archivo `build.gradle`. La configuración `apt` se utiliza para configurar los procesadores de anotación que se utilizarán. En el ejemplo anterior, el procesador de anotaciones `autoservicio` está configurado.

El procesador de anotaciones `auto-service` se utiliza para generar código para la anotación `@AutoService`. La anotación `@AutoService` se utiliza para anotar una clase que debe registrarse con un proveedor de `autoservicio`.

El proveedor de `auto-servicio` es un servicio que proporciona una lista de clases que han sido anotadas con la anotación `@AutoService`. El proveedor de `servicio automático` se puede utilizar para generar código para una interfaz de proveedor de servicios (SPI).

En el ejemplo anterior, la anotación `@AutoService` se usa para anotar una clase que debe registrarse con el proveedor de `autoservicio`. El proveedor de `autoservicio` generará código para la interfaz `com.google.auto.service.AutoService`.

La interfaz `com.google.auto.service.AutoService` es un SPI que se utiliza para registrar clases con el proveedor de `autoservicio`. El proveedor de `autoservicio` usará la interfaz `com.google.auto.service.AutoService` para generar código para el archivo `META-INF/services/`.

El archivo `META-INF/services/` se utiliza para almacenar una lista de clases que se han registrado con el proveedor de `autoservicio`. El archivo `META-INF/services/` es utilizado por `java.util.ServiceLoader` para cargar clases de un proveedor de servicios.

En el ejemplo anterior, el archivo `META-INF/services/` contendrá lo siguiente:

```
com.google.auto.service.AutoService
com.example.MyClass
```

El `java.util.ServiceLoader` usará el archivo `META-INF/services/` para cargar la clase `com.example.MyClass`. La clase `com.example.MyClass` se registrará con el proveedor de `autoservicio`.

El proveedor de `autoservicio` generará código para la interfaz `com.google.auto.service.AutoService`. La interfaz `com.google.auto.service.AutoService` se utiliza para registrar clases con el proveedor de `autoservicio`.

En el ejemplo anterior, la interfaz `com.google.auto.service.AutoService` se usa para registrar la clase `com.example.MyClass` con el proveedor `auto-service`. El proveedor de `autoservicio` generará código para el archivo `META-INF/services/`.

El archivo `META-INF/services/` se utiliza para almacenar una lista de clases que se han registrado con el proveedor de `autoservicio`. El archivo `META-INF/services/` es utilizado por `java.util.ServiceLoader` para cargar clases de un proveedor de servicios.

En el ejemplo anterior, el archivo `META-INF/services/` contendrá lo siguiente:

```
com.google.auto.service.AutoService
com.example.MyClass
```

El `java.util.ServiceLoader` usará el archivo `META-INF/services/` para cargar la clase `com.example.MyClass`. La clase `com.example.MyClass` se registrará con el proveedor de `autoservicio`.

## Conclusión

El procesamiento de anotaciones es una forma de generar código en tiempo de compilación. En Kotlin, el procesamiento de anotaciones se realiza mediante el complemento kotlin-apt. El complemento kotlin-apt es un complemento del compilador de Kotlin que agrega soporte para el procesamiento de anotaciones.

El complemento kotlin-apt agrega una configuración `apt` al archivo `build.gradle`. La configuración `apt` se utiliza para configurar los procesadores de anotación que se utilizarán. En el ejemplo anterior, el procesador de anotaciones `autoservicio` está configurado.

El procesador de anotaciones `auto-service` se utiliza para generar código para la anotación `@AutoService`. La anotación `@AutoService` se utiliza para anotar una clase que debe registrarse con un proveedor de `autoservicio`.

El proveedor de `auto-servicio` es un servicio que proporciona una lista de clases que han sido anotadas con la anotación `@AutoService`. El proveedor de `servicio automático` se puede utilizar para generar código para una interfaz de proveedor de servicios (SPI).

En el ejemplo anterior, la anotación `@AutoService` se usa para anotar una clase que debe registrarse con el proveedor de `autoservicio`. El proveedor de `autoservicio` generará código para la interfaz `com.google.auto.service.AutoService`.

La interfaz `com.google.auto.service.AutoService` es un SPI que se utiliza para registrar clases con el proveedor de `autoservicio`. El proveedor de `autoservicio` usará la interfaz `com.google.auto.service.AutoService` para generar código para el archivo `META-INF/services/`.

El archivo `META-INF/services/` se utiliza para almacenar una lista de clases que se han registrado con el proveedor de `autoservicio`. El archivo `META-INF/services/` es utilizado por `java.util.ServiceLoader` para cargar clases de un proveedor de servicios.

En el ejemplo anterior, el archivo `META-INF/services/` contendrá lo siguiente:

```
com.google.auto.service.AutoService
com.example.MyClass
```

El `java.util.ServiceLoader` usará el archivo `META-INF/services/` para cargar la clase `com.example.MyClass`. La clase `com.example.MyClass` se registrará con el proveedor de `autoservicio`.

El proveedor de `autoservicio` generará código para la interfaz `com.google.auto.service.AutoService`. La interfaz `com.google.auto.service.AutoService` se utiliza para registrar clases con el proveedor de `autoservicio`.

En el ejemplo anterior, la interfaz `com.google.auto.service.AutoService` se usa para registrar la clase `com.example.MyClass` con el proveedor `auto-service`. El proveedor de `autoservicio` generará código para el archivo `META-INF/services/`.

El archivo `META-INF/services/` se utiliza para almacenar una lista de clases que se han registrado con el proveedor de `autoservicio`. El archivo `META-INF/services/` es utilizado por `java.util.ServiceLoader` para cargar clases de un proveedor de servicios.

En el ejemplo anterior, el archivo `META-INF/services/` contendrá lo siguiente:

```
com.google.auto.service.AutoService
com.example.MyClass
```

El `java.util.ServiceLoader` usará el archivo `META-INF/services/` para cargar la clase `com.example.MyClass`. La clase `com.example.MyClass` se registrará con el proveedor de `autoservicio`.