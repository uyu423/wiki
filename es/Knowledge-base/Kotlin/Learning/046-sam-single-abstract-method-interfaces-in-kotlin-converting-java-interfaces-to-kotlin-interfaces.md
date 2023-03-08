---
title: 046: Interfaces SAM (método abstracto único) en Kotlin: conversión de interfaces Java a interfaces Kotlin
description: 
published: true
date: 2023-02-05T21:55:17.936Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:55:16.377Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [046: SAM (Single Abstract Method) Interfaces in Kotlin: Converting Java Interfaces to Kotlin Interfaces***English** document is available*](/en/Knowledge-base/Kotlin/Learning/046-sam-single-abstract-method-interfaces-in-kotlin-converting-java-interfaces-to-kotlin-interfaces)
{.links-list}


# 046: Interfaces SAM (Single Abstract Method) en Kotlin: Conversión de interfaces Java a interfaces Kotlin

Como Kotlin es un lenguaje JVM, es totalmente compatible con Java. Esto significa que puede tomar cualquier interfaz de Java y convertirla en una interfaz de Kotlin sin ningún problema.

Sin embargo, hay una advertencia: Kotlin no es compatible con las interfaces SAM (Single Abstract Method). Esto significa que no puede tomar una interfaz de Java con un único método abstracto y convertirla en una interfaz de Kotlin.

La razón de esto es que el sistema de tipos de Kotlin es diferente al de Java. En Kotlin, cada interfaz debe tener al menos un método abstracto, incluso si es solo un método ficticio sin cuerpo.

Esto no es un problema si está convirtiendo una interfaz Java con múltiples métodos abstractos a Kotlin. Sin embargo, si está convirtiendo una interfaz SAM, deberá agregar un método abstracto a la interfaz de Kotlin.

No hay una manera fácil de hacer esto, por lo que deberá agregar el método abstracto manualmente. La mejor manera de hacer esto es agregar un método ficticio sin cuerpo. Esto garantizará que la interfaz de Kotlin sea compatible con la interfaz de Java.

Aquí hay un ejemplo de una interfaz Java SAM:

```java
public interface Runnable {
     public void run();
}
```

Y aquí está la interfaz Kotlin equivalente:

```kotlin
interface Runnable {
    fun run()
}
```

Como puede ver, la interfaz de Kotlin tiene un método extra abstracto, ```run()```, que es requerido por el sistema de tipos de Kotlin.

Si está convirtiendo una interfaz Java a Kotlin, siempre debe verificar si la interfaz es una interfaz SAM. Si es así, deberá agregar un método abstracto adicional a la interfaz de Kotlin.