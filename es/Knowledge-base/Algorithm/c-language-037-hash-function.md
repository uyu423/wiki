---
title: [Lenguaje C] 037: función hash
description: 
published: true
date: 2023-02-13T17:32:38.107Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:32:30.976Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 037: Hash Function***English** document is available*](/en/Knowledge-base/Algorithm/c-language-037-hash-function)
{.links-list}


# Función hash

Una función hash es una función matemática que convierte un valor en un hash, que es un valor numérico de tamaño fijo. Las funciones hash se utilizan en diversas áreas de la informática, como estructuras de datos, criptografía y teoría de la información.

Hay muchos tipos diferentes de funciones hash, pero todas tienen un objetivo: tomar algunos datos de entrada y asignarlos a una salida pequeña y de tamaño fijo. La salida de una función hash generalmente se denomina valor hash, código hash o simplemente hash.

Las funciones hash son una parte crítica de muchas aplicaciones informáticas. Por ejemplo, las tablas hash son estructuras de datos que utilizan funciones hash para almacenar y recuperar datos. Las funciones hash también se utilizan en criptografía para firmas digitales y códigos de autenticación de mensajes (MAC).

## Cómo funcionan las funciones hash

Para entender cómo funcionan las funciones hash, veamos un ejemplo simple. Supongamos que tenemos una lista de nombres de estudiantes y números de identificación, y queremos almacenar estos datos en una tabla hash. Podemos usar una función hash para asignar el nombre de cada estudiante a un número de identificación.

Para hacer esto, primero debemos elegir una función hash. Hay muchas funciones hash diferentes para elegir, pero para este ejemplo, usaremos la función hash de módulo. Esta función toma un valor de entrada y lo divide por el tamaño de la tabla hash. El resto es el valor hash.

Por ejemplo, supongamos que el tamaño de nuestra tabla hash es 10. Si usamos la función hash de módulo para asignar el nombre del estudiante "John Smith" a un valor hash, obtenemos lo siguiente:

```
Hash("John Smith") = ("John Smith" % 10) = 2
```

Esto significa que el nombre del estudiante "John Smith" se almacenará en la ranura 2 de la tabla hash.

Podemos usar la misma función hash para asignar el nombre del estudiante "Mary Johnson" a un valor hash:

```
Hash("Mary Johnson") = ("Mary Johnson" % 10) = 3
```

Esto significa que el nombre del estudiante "Mary Johnson" se almacenará en la ranura 3 de la tabla hash.

## Elegir una función hash

Hay muchas funciones hash diferentes para elegir. El criterio más importante para una función hash es que debe ser fácil de calcular. La función hash de módulo que usamos en el ejemplo anterior es una función hash simple, pero tiene algunos inconvenientes.

Primero, la función hash de módulo solo se puede usar si el tamaño de la tabla hash es una potencia de dos. Esto se debe a que el operador módulo solo funciona en potencias de dos.

En segundo lugar, la función hash de módulo puede producir muchas colisiones. Se produce una colisión cuando dos o más valores de entrada se asignan al mismo valor hash. Por ejemplo, si usamos la función hash de módulo para asignar los nombres de los estudiantes "John Smith" y "Jane Doe" a valores hash, obtenemos lo siguiente:

```
Hash("John Smith") = ("John Smith" % 10) = 2
Hash("Jane Doe") = ("Jane Doe" % 10) = 2
```

Tanto "John Smith" como "Jane Doe" están asignados al valor hash 2, por lo que tenemos una colisión.

Hay muchas formas de evitar colisiones, pero la forma más común es usar una tabla hash más grande. Una tabla hash más grande significa que hay más ranuras para asignar valores de entrada, por lo que se reducen las posibilidades de colisión.

## Funciones hash en criptografía

Las funciones hash también se utilizan en criptografía. Por ejemplo, una firma digital es un valor hash que se calcula a partir de algunos datos de entrada, como un documento. A continuación, la firma se cifra con la clave privada del remitente.

Cuando el receptor obtiene la firma, puede descifrarla con la clave pública del remitente. Luego pueden calcular el valor hash de los datos de entrada y compararlo con la firma descifrada. Si los dos valores coinciden, los datos no se han manipulado y su uso es seguro.

Las funciones hash también se utilizan en los códigos de autenticación de mensajes (MAC). Un MAC es un valor hash que se calcula a partir de algunos datos de entrada, como un mensaje y una clave secreta. Luego, el MAC se envía junto con el mensaje.

Cuando el receptor recibe el mensaje, puede calcular el MAC a partir del mensaje y la clave secreta. Luego pueden comparar la MAC calculada con la MAC que se envió junto con el mensaje. Si los dos MAC coinciden, entonces el mensaje no ha sido manipulado y es seguro de usar.

## Conclusión

Las funciones hash son funciones matemáticas que asignan valores de entrada a valores hash. Las funciones hash se utilizan en diversas áreas de la informática, como estructuras de datos, criptografía y teoría de la información.

Hay muchos tipos diferentes de funciones hash, pero todas tienen un objetivo: tomar algunos datos de entrada y asignarlos a una salida pequeña y de tamaño fijo. La salida de una función hash generalmente se denomina valor hash, código hash o simplemente hash.

Las funciones hash son una parte crítica de muchas aplicaciones informáticas. Por ejemplo, las tablas hash son estructuras de datos que utilizan funciones hash para almacenar y recuperar datos. Las funciones hash también se utilizan en criptografía para firmas digitales y códigos de autenticación de mensajes (MAC).