---
title: 039: Constructores en Kotlin: inicialización de clases con diferentes constructores
description: 
published: true
date: 2023-02-16T11:32:51.449Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:32:49.865Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [039: Constructors in Kotlin: Initializing Classes with Different Constructors***English** document is available*](/en/Knowledge-base/Kotlin/Learning/039-constructors-in-kotlin-initializing-classes-with-different-constructors)
{.links-list}


# 039: Constructores en Kotlin: Inicializando Clases con Diferentes Constructores

Kotlin ofrece una amplia variedad de opciones cuando se trata de inicializar clases. En esta publicación, veremos los constructores en Kotlin y cómo se pueden usar para inicializar clases con diferentes valores.

Los constructores son funciones especiales que se utilizan para inicializar clases. En Kotlin, hay dos tipos de constructores: primarios y secundarios. El constructor primario es el que se usa para inicializar la clase cuando se crea por primera vez. Se declara en la parte superior de la clase, antes del cuerpo de la clase.

Los constructores secundarios se utilizan para inicializar la clase con diferentes valores. Se declaran dentro del cuerpo de la clase.

Las clases pueden tener varios constructores secundarios, pero todos deben llamar al constructor principal. Esto asegura que la clase siempre se inicialice con al menos los valores predeterminados.

Para crear una clase con un constructor principal, usamos la palabra clave `clase` seguida del nombre de la clase. Luego declaramos el constructor principal entre paréntesis. Dentro del constructor principal, podemos declarar cualquier número de parámetros. Estos parámetros pueden ser val o var.

```kotlin
class MyClass(val param1: String, var param2: Int) {

}
```

En el ejemplo anterior, hemos creado una clase llamada `MyClass` con un constructor principal que toma dos parámetros. El primer parámetro es `val` y el segundo es `var`.

También podemos crear una clase sin un constructor principal. En este caso, la clase se inicializará con los valores por defecto de cada uno de los parámetros.

```kotlin
class MyClass {

}
```

Para crear un constructor secundario, usamos la palabra clave `constructor` seguida de los parámetros entre paréntesis. Luego podemos inicializar la clase con diferentes valores dentro del cuerpo del constructor secundario.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

}
```

En el ejemplo anterior, hemos creado un constructor secundario que toma un solo parámetro. Este constructor llama al constructor principal y pasa el valor predeterminado para el segundo parámetro.

También podemos crear una clase con múltiples constructores secundarios. En este caso, cada constructor secundario debe llamar a un constructor secundario diferente.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

En el ejemplo anterior, hemos creado una clase con dos constructores secundarios. El primer constructor llama al constructor primario y el segundo constructor llama al primer constructor secundario.

También podemos crear una clase con un constructor primario y múltiples constructores secundarios. En este caso, cada constructor secundario debe llamar al constructor principal.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

En el ejemplo anterior, hemos creado una clase con un constructor primario y dos constructores secundarios. El primer constructor secundario llama al constructor principal y el segundo constructor secundario llama al primer constructor secundario.

También podemos crear una clase con un constructor primario y múltiples constructores secundarios. En este caso, cada constructor secundario debe llamar a un constructor secundario diferente.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

En el ejemplo anterior, hemos creado una clase con un constructor primario y dos constructores secundarios. El primer constructor secundario llama al constructor principal y el segundo constructor secundario llama al primer constructor secundario.

También podemos crear una clase con un constructor primario y múltiples constructores secundarios. En este caso, cada constructor secundario debe llamar al constructor primario.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

En el ejemplo anterior, hemos creado una clase con un constructor primario y dos constructores secundarios. El primer constructor secundario llama al constructor principal y el segundo constructor secundario llama al primer constructor secundario.