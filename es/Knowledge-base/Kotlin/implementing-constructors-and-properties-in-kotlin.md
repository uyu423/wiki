---
title: Implementación de constructores y propiedades en Kotlin
description: 
published: true
date: 2023-02-02T02:18:21.246Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:18:19.498Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Implementing Constructors and Properties in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/implementing-constructors-and-properties-in-kotlin)
{.links-list}


# Implementación de constructores y propiedades en Kotlin

Kotlin es un lenguaje de programación relativamente nuevo que ha ido ganando popularidad en la comunidad de desarrollo. Es un lenguaje orientado a objetos y tipado estáticamente que se ejecuta en la máquina virtual de Java. Kotlin es compatible con todas las bibliotecas y marcos de Java existentes y se puede utilizar para una amplia gama de tareas de desarrollo.

Una de las principales características de Kotlin es su compatibilidad con la programación basada en constructores. En Kotlin, las clases pueden tener uno o más constructores. El constructor principal se define en el encabezado de la clase y los constructores secundarios se definen dentro del cuerpo de la clase.

Los constructores se utilizan para inicializar objetos de una clase. Se pueden usar para establecer valores iniciales para variables, invocar métodos, etc. En Kotlin, no se requieren constructores si la clase no tiene inicializadores. Sin embargo, si una clase tiene inicializadores, se debe definir al menos un constructor.

El siguiente es un ejemplo simple de una clase de Kotlin con un constructor principal y dos constructores secundarios:

```kotlin
class Person(val name: String) {
  
    var age: Int = 0
    
    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
    
    constructor(name: String, age: Int, gender: String) : this(name, age) {
        // ...
    }
}
```

En el ejemplo anterior, el constructor principal toma un solo argumento, nombre. Los constructores secundarios toman dos y tres argumentos, respectivamente. Todos los constructores llaman al constructor principal usando la palabra clave this.

Los constructores también se pueden usar para inicializar las propiedades de una clase. En el ejemplo anterior, el constructor principal inicializa la propiedad de nombre y los constructores secundarios inicializan la propiedad de edad.

Otra característica de Kotlin es su soporte para propiedades. Las propiedades son variables que están asociadas con una clase. Se pueden declarar en el encabezado de la clase o en el cuerpo de la clase.

El siguiente es un ejemplo simple de una clase Kotlin con dos propiedades, nombre y edad:

```kotlin
class Person {
  
    var name: String = ""
    
    var age: Int = 0
}
```

En el ejemplo anterior, las propiedades de nombre y edad se declaran en el encabezado de la clase. Ambos se inicializan con los valores predeterminados de "" y 0, respectivamente.

Las propiedades también se pueden inicializar con valores no predeterminados. En el siguiente ejemplo, la propiedad de nombre se inicializa con el valor "John" y la propiedad de edad se inicializa con el valor 30:

```kotlin
class Person {
  
    var name: String = "John"
    
    var age: Int = 30
}
```

Kotlin también admite la inicialización diferida de propiedades. La inicialización diferida es una técnica para retrasar la inicialización de una propiedad hasta que se accede a ella por primera vez. En Kotlin, la inicialización diferida se logra mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad inicializada diferida, nombre:

```kotlin
class Person {
  
    val name: String by lazy {
        // ...
    }
}
```

En el ejemplo anterior, la propiedad de nombre se declara como val (inmutable) y se inicializa de forma diferida. El inicializador es una expresión lambda que se invoca cuando se accede a la propiedad por primera vez.

Kotlin también admite propiedades delegadas. Las propiedades delegadas son propiedades implementadas por un objeto delegado. En Kotlin, las propiedades delegadas se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad delegada, nombre:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

En el ejemplo anterior, la propiedad de nombre se implementa mediante un objeto delegado. El objeto delegado se inicializa de forma perezosa mediante una expresión lambda.

Kotlin también admite propiedades de extensión. Las propiedades de extensión son propiedades que se declaran como extensiones de una clase. En Kotlin, las propiedades de extensión se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de extensión, nombre:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

En el ejemplo anterior, la propiedad de nombre se amplía mediante una expresión lambda diferida que invoca el método extension().

Kotlin también admite propiedades inicializadas en pizarra. Las propiedades con inicialización tardía son propiedades que no se inicializan hasta que se accede a ellas por primera vez. En Kotlin, las propiedades de inicialización tardía se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de inicialización tardía, nombre:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

En el ejemplo anterior, la propiedad de nombre se declara como lateinit var (mutable). No se inicializa hasta que se invoca el método init().

Kotlin también admite tipos anulables. Los tipos anulables son tipos que pueden contener el valor nulo. En Kotlin, los tipos que aceptan valores NULL se declaran con el ? operador.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad anulable, nombre:

```kotlin
class Person {
  
    var name: String? = null
}
```

En el ejemplo anterior, la propiedad de nombre se declara como un tipo anulable. Puede mantener el valor nulo.

Kotlin también admite propiedades inmutables. Las propiedades inmutables son propiedades que no se pueden cambiar después de inicializarse. En Kotlin, las propiedades inmutables se declaran con la palabra clave val.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad inmutable, nombre:

```kotlin
class Person(val name: String) {
  
}
```

En el ejemplo anterior, la propiedad de nombre se declara como val (inmutable). No se puede cambiar después de inicializarlo.

Kotlin también admite propiedades mutables. Las propiedades mutables son propiedades que se pueden cambiar después de inicializarse. En Kotlin, las propiedades mutables se declaran con la palabra clave var.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad mutable, nombre:

```kotlin
class Person {
  
    var name: String = ""
}
```

En el ejemplo anterior, la propiedad de nombre se declara como var (mutable). Se puede cambiar después de inicializarlo.

Kotlin también admite campos de respaldo. Los campos de respaldo son variables que se utilizan para almacenar los valores de las propiedades. En Kotlin, los campos de respaldo se declaran usando la palabra clave de campo.

El siguiente es un ejemplo simple de una clase de Kotlin con un campo de respaldo, nombre:

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

En el ejemplo anterior, la propiedad de nombre tiene un campo de respaldo. El campo de respaldo se declara como un conjunto privado, lo que significa que solo puede ser modificado por el setter de la propiedad.

Kotlin también admite propiedades delegadas. Las propiedades delegadas son propiedades implementadas por un objeto delegado. En Kotlin, las propiedades delegadas se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad delegada, nombre:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

En el ejemplo anterior, la propiedad de nombre se implementa mediante un objeto delegado. El objeto delegado se inicializa de forma perezosa mediante una expresión lambda.

Kotlin también admite propiedades de extensión. Las propiedades de extensión son propiedades que se declaran como extensiones de una clase. En Kotlin, las propiedades de extensión se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de extensión, nombre:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

En el ejemplo anterior, la propiedad de nombre se amplía mediante una expresión lambda diferida que invoca el método extension().

Kotlin también admite propiedades inicializadas en pizarra. Las propiedades con inicialización tardía son propiedades que no se inicializan hasta que se accede a ellas por primera vez. En Kotlin, las propiedades de inicialización tardía se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de inicialización tardía, nombre:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

En el ejemplo anterior, la propiedad de nombre se declara como lateinit var (mutable). No se inicializa hasta que se invoca el método init().

Kotlin también admite tipos anulables. Los tipos anulables son tipos que pueden contener el valor nulo. En Kotlin, los tipos que aceptan valores NULL se declaran con el ? operador.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad anulable, nombre:

```kotlin
class Person {
  
    var name: String? = null
}
```

En el ejemplo anterior, la propiedad de nombre se declara como un tipo anulable. Puede mantener el valor nulo.

Kotlin también admite propiedades inmutables. Las propiedades inmutables son propiedades que no se pueden cambiar después de inicializarse. En Kotlin, las propiedades inmutables se declaran con la palabra clave val.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad inmutable, nombre:

```kotlin
class Person(val name: String) {
  
}
```

En el ejemplo anterior, la propiedad de nombre se declara como val (inmutable). No se puede cambiar después de inicializarlo.

Kotlin también admite propiedades mutables. Las propiedades mutables son propiedades que se pueden cambiar después de inicializarse. En Kotlin, las propiedades mutables se declaran con la palabra clave var.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad mutable, nombre:

```kotlin
class Person {
  
    var name: String = ""
}
```

En el ejemplo anterior, la propiedad de nombre se declara como var (mutable). Se puede cambiar después de inicializarlo.

Kotlin también admite campos de respaldo. Los campos de respaldo son variables que se utilizan para almacenar los valores de las propiedades. En Kotlin, los campos de respaldo se declaran usando la palabra clave de campo.

El siguiente es un ejemplo simple de una clase de Kotlin con un campo de respaldo, nombre:

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

En el ejemplo anterior, la propiedad de nombre tiene un campo de respaldo. El campo de respaldo se declara como un conjunto privado, lo que significa que solo puede ser modificado por el setter de la propiedad.

Kotlin también admite propiedades delegadas. Las propiedades delegadas son propiedades implementadas por un objeto delegado. En Kotlin, las propiedades delegadas se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad delegada, nombre:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

En el ejemplo anterior, la propiedad de nombre se implementa mediante un objeto delegado. El objeto delegado se inicializa de forma perezosa mediante una expresión lambda.

Kotlin también admite propiedades de extensión. Las propiedades de extensión son propiedades que se declaran como extensiones de una clase. En Kotlin, las propiedades de extensión se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de extensión, nombre:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

En el ejemplo anterior, la propiedad de nombre se amplía mediante una expresión lambda diferida que invoca el método extension().

Kotlin también admite propiedades inicializadas en pizarra. Las propiedades con inicialización tardía son propiedades que no se inicializan hasta que se accede a ellas por primera vez. En Kotlin, las propiedades de inicialización tardía se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de inicialización tardía, nombre:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

En el ejemplo anterior, la propiedad de nombre se declara como lateinit var (mutable). No se inicializa hasta que se invoca el método init().

Kotlin también admite tipos anulables. Los tipos anulables son tipos que pueden contener el valor nulo. En Kotlin, los tipos que aceptan valores NULL se declaran con el ? operador.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad anulable, nombre:

```kotlin
class Person {
  
    var name: String? = null
}
```

En el ejemplo anterior, la propiedad de nombre se declara como un tipo anulable. Puede mantener el valor nulo.

Kotlin también admite propiedades inmutables. Las propiedades inmutables son propiedades que no se pueden cambiar después de inicializarse. En Kotlin, las propiedades inmutables se declaran con la palabra clave val.

El siguiente es un ejemplo simple de una clase Kotlin con una propiedad inmutable, nombre:

```kotlin
class Person(val name: String) {
  
}
```

En el ejemplo anterior, la propiedad de nombre se declara como val (inmutable). No se puede cambiar después de inicializarlo.

Kotlin también admite propiedades mutables. Las propiedades mutables son propiedades que se pueden cambiar después de inicializarse. En Kotlin, las propiedades mutables se declaran con la palabra clave var.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad mutable, nombre:

```kotlin
class Person {
  
    var name: String = ""
}
```

En el ejemplo anterior, la propiedad de nombre se declara como var (mutable). Se puede cambiar después de inicializarlo.

Kotlin también admite campos de respaldo. Los campos de respaldo son variables que se utilizan para almacenar los valores de las propiedades. En Kotlin, los campos de respaldo se declaran usando la palabra clave de campo.

El siguiente es un ejemplo simple de una clase de Kotlin con un campo de respaldo, nombre:

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

En el ejemplo anterior, la propiedad de nombre tiene un campo de respaldo. El campo de respaldo se declara como un conjunto privado, lo que significa que solo puede ser modificado por el setter de la propiedad.

Kotlin también admite propiedades delegadas. Las propiedades delegadas son propiedades implementadas por un objeto delegado. En Kotlin, las propiedades delegadas se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad delegada, nombre:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

En el ejemplo anterior, la propiedad de nombre se implementa mediante un objeto delegado. El objeto delegado se inicializa de forma perezosa mediante una expresión lambda.

Kotlin también admite propiedades de extensión. Las propiedades de extensión son propiedades que se declaran como extensiones de una clase. En Kotlin, las propiedades de extensión se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de extensión, nombre:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

En el ejemplo anterior, la propiedad de nombre se amplía mediante una expresión lambda diferida que invoca el método extension().

Kotlin también admite propiedades inicializadas en pizarra. Las propiedades con inicialización tardía son propiedades que no se inicializan hasta que se accede a ellas por primera vez. En Kotlin, las propiedades de inicialización tardía se declaran mediante la palabra clave by.

El siguiente es un ejemplo simple de una clase de Kotlin con una propiedad de inicialización tardía, nombre:

```kotlin
Persona de clase {
  
    lateinit var nombre: Cadena
    
    inicio divertido () {
        nombre = "Juan"
    }
}
``