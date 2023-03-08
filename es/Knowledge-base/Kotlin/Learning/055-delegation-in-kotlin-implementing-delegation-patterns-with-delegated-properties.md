---
title: 055: Delegación en Kotlin: Implementación de patrones de delegación con propiedades delegadas
description: 
published: true
date: 2023-02-16T19:32:27.774Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:32:26.216Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [055: Delegation in Kotlin: Implementing Delegation Patterns with Delegated Properties***English** document is available*](/en/Knowledge-base/Kotlin/Learning/055-delegation-in-kotlin-implementing-delegation-patterns-with-delegated-properties)
{.links-list}


# Delegación en Kotlin: Implementación de patrones de delegación con propiedades delegadas

Kotlin proporciona poderosos mecanismos de delegación que se pueden usar para implementar varios patrones de delegación. En esta publicación, veremos cómo usar las propiedades delegadas para implementar el patrón de delegación en Kotlin.

La delegación es un patrón de diseño de software que permite que un objeto delegue la responsabilidad de ciertas tareas a otro objeto. La delegación se puede utilizar para mejorar la modularidad y la reutilización del código.

Hay muchos patrones de delegación diferentes, pero el más común es el patrón de delegación. En el patrón de delegación, un objeto (el "delegado") es responsable de manejar una solicitud de otro objeto (el "solicitante").

El patrón de delegación se usa a menudo en la programación orientada a objetos para mejorar la modularidad del código. Por ejemplo, si tiene una clase que necesita realizar una tarea compleja, puede delegar esa tarea a otra clase. Esto le permite reutilizar el código de la clase delegada en otras clases.

La delegación también se puede utilizar para mejorar la reutilización del código. Por ejemplo, si tiene una clase que necesita realizar una tarea que no es específica de esa clase, puede delegar esa tarea a otra clase. Esto le permite reutilizar el código de la clase delegada en otras clases.

La delegación es una herramienta poderosa, pero puede ser mal utilizada. Por ejemplo, si delega una tarea a una clase que no es adecuada para esa tarea, el código de la clase delegada puede volverse complicado y difícil de mantener.

Cuando se usa correctamente, la delegación puede ser una herramienta muy poderosa para mejorar la modularidad y la reutilización del código. En esta publicación, veremos cómo usar las propiedades delegadas para implementar el patrón de delegación en Kotlin.

Las propiedades delegadas son una característica poderosa de Kotlin que le permite delegar la responsabilidad de una propiedad a otro objeto. Las propiedades delegadas se declaran mediante la palabra clave by. Por ejemplo, el siguiente código declara una propiedad delegada de tipo String:

```kotlin
class MyClass {
    val delegatedProperty: String by Delegate()
}
```

En el código anterior, la propiedad delegatedProperty se delega a una instancia de la clase Delegate. La clase Delegado debe implementar los métodos getValue() y setValue(). Estos métodos se utilizan para obtener y establecer el valor de la propiedad delegada, respectivamente.

Los métodos getValue() y setValue() toman dos argumentos: la instancia de la clase que posee la propiedad delegada y el valor de la propiedad delegada. Por ejemplo, el siguiente código muestra cómo se pueden implementar los métodos getValue() y setValue():

```kotlin
class Delegate {
    fun getValue(thisRef: Any, property: KProperty<*>): String {
        // return the value of the delegated property
    }

    fun setValue(thisRef: Any, property: KProperty<*>, value: String) {
        // set the value of the delegated property
    }
}
```

En el código anterior, los métodos getValue() y setValue() se implementan en la clase Delegate. Estos métodos toman dos argumentos: la instancia de la clase que posee la propiedad delegada y el valor de la propiedad delegada.

El método getValue() se usa para obtener el valor de la propiedad delegada. El método setValue() se usa para establecer el valor de la propiedad delegada.

Las propiedades delegadas son una característica poderosa de Kotlin que se puede usar para implementar el patrón de delegación. En la siguiente sección, veremos cómo usar las propiedades delegadas para implementar un patrón de delegación simple.