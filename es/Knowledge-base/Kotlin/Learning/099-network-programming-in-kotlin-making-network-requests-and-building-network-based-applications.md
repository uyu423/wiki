---
title: 099: Programación de red en Kotlin: Realización de solicitudes de red y creación de aplicaciones basadas en red
description: 
published: true
date: 2023-02-16T09:17:45.580Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:17:43.388Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [099: Network Programming in Kotlin: Making Network Requests and Building Network-based Applications***English** document is available*](/en/Knowledge-base/Kotlin/Learning/099-network-programming-in-kotlin-making-network-requests-and-building-network-based-applications)
{.links-list}


# 099: Programación de red en Kotlin: Realización de solicitudes de red y creación de aplicaciones basadas en red

Kotlin es un poderoso lenguaje de programación que se puede usar para crear una variedad de aplicaciones, incluidas las aplicaciones basadas en red. En esta publicación, veremos cómo usar Kotlin para realizar solicitudes de red y crear aplicaciones basadas en red.

## Realización de solicitudes de red

Una de las tareas más comunes cuando se trabaja con aplicaciones basadas en red es realizar solicitudes de red. Kotlin facilita la realización de solicitudes de red mediante la clase integrada [`HttpURLConnection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/).

Para realizar una solicitud de red, primero debemos crear una instancia `HttpURLConnection`. Podemos hacer esto pasando la URL del recurso que queremos solicitar:

```kotlin
val url = "https://www.example.com"
val connection = HttpURLConnection(url)
```

Una vez que tengamos una instancia de `HttpURLConnection`, podemos usar [`setRequestMethod`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request- method.html) para establecer el método de solicitud. El método de solicitud determina el tipo de acción que se llevará a cabo en el recurso. Los métodos de solicitud más comunes son `GET`, `POST`, `PUT` y `DELETE`.

```kotlin
connection.setRequestMethod("GET")
```

También podemos usar el método [`setRequestProperty`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request-property.html) para configurar la solicitud encabezados Los encabezados de solicitud se utilizan para proporcionar información adicional sobre la solicitud, como el tipo de contenido que se solicita.

```kotlin
connection.setRequestProperty("Content-Type", "application/json")
```

Una vez que hayamos configurado la instancia `HttpURLConnection`, podemos usar [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/get-input -stream.html) para obtener el flujo de entrada para la conexión. El flujo de entrada se puede utilizar para leer la respuesta del servidor.

```kotlin
val inputStream = connection.getInputStream()
```

## Creación de aplicaciones basadas en red

Además de realizar solicitudes de red, Kotlin también se puede utilizar para crear aplicaciones basadas en red. Kotlin proporciona una clase [`Socket`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/) que se puede usar para crear aplicaciones basadas en socket.

Para crear una aplicación basada en socket, primero debemos crear una instancia `Socket`. Podemos hacer esto pasando el nombre de host y el número de puerto del servidor al que queremos conectarnos:

```kotlin
val socket = Socket("www.example.com", 80)
```

Una vez que tengamos una instancia de `Socket`, podemos usar [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-input-stream.html) y [`getOutputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-output-stream.html) para obtener los flujos de entrada y salida para el socket. Estos flujos se pueden utilizar para enviar y recibir datos a través de la conexión de socket.

```kotlin
val inputStream = socket.getInputStream()
val outputStream = socket.getOutputStream()
```

Una vez que tengamos los flujos de entrada y salida, podemos usar [`write`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-output-stream/write.html) y [ `read`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-input-stream/read.html) métodos para enviar y recibir datos a través de la conexión de socket.

```kotlin
outputStream.write("Hello, world!".toByteArray())

val response = inputStream.read()
```

Finalmente, podemos usar el método [`close`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/close.html) para cerrar la conexión del socket.

```kotlin
socket.close()
```

## Conclusión

En esta publicación, analizamos cómo usar Kotlin para realizar solicitudes de red y crear aplicaciones basadas en red. El soporte de Kotlin para la programación en red lo convierte en una excelente opción para crear una variedad de aplicaciones.