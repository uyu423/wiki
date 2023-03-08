---
title: Coroutines de Kotlin para el desarrollo asincrónico del lado del servidor
description: 
published: true
date: 2023-02-04T10:17:45.362Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:17:43.641Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin Coroutines for Asynchronous Server-side Development***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-coroutines-for-asynchronous-server-side-development)
{.links-list}


# Coroutines de Kotlin para el desarrollo asíncrono del lado del servidor

Las corrutinas de Kotlin brindan una forma eficiente de administrar la concurrencia en el lado del servidor. Mediante el uso de corrutinas, los desarrolladores pueden escribir código que responda mejor a la entrada del usuario y, al mismo tiempo, brinden una experiencia rica al usuario.

Las rutinas se introdujeron en Kotlin 1.1 y han sido una característica estable desde Kotlin 1.3. En el contexto de la corrutina, una corrutina es un subproceso liviano que se puede usar para descargar trabajo del subproceso principal. Esto permite a los desarrolladores escribir código que responda mejor a la entrada del usuario, al mismo tiempo que proporciona una experiencia de usuario rica.

Las corrutinas se pueden usar con cualquier biblioteca Java existente, lo que las convierte en una excelente herramienta para el desarrollo asíncrono del lado del servidor. En este artículo, veremos cómo usar rutinas en una aplicación web Java.

## Configuración del proyecto

Comenzaremos configurando un proyecto Maven simple. Agregue las siguientes dependencias a su `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.jetbrains.kotlin</groupId>
        <artifactId>kotlin-stdlib-jdk8</artifactId>
        <version>1.3.72</version>
    </dependency>
    <dependency>
        <groupId>org.jetbrains.kotlinx</groupId>
        <artifactId>kotlinx-coroutines-core</artifactId>
        <version>1.3.7</version>
    </dependency>
</dependencies>
```

Estamos usando Kotlin 1.3.72 y Kotlinx Coroutines 1.3.7. La dependencia `kotlin-stdlib-jdk8` incluye la biblioteca estándar de Kotlin, mientras que la dependencia `kotlinx-coroutines-core` proporciona la funcionalidad principal de coroutine.

## Crear una rutina

Las corrutinas se pueden crear usando las funciones `launch` o `async` del paquete `kotlinx.coroutines`. La función `lanzar` crea una nueva rutina y la inicia inmediatamente. La función `async` crea una nueva rutina, pero no la inicia inmediatamente. En su lugar, devuelve una instancia de la clase `Deferred`, que se puede usar para iniciar la rutina más tarde.

Por ejemplo, podemos crear una corrutina que duerma durante un segundo usando la función `lanzar`:

```kotlin
import kotlinx.coroutines.*

fun main() {
    launch {
        // Suspend this coroutine for one second
        delay(1000)
        println("Hello, world!")
    }
}
```

También podemos crear una corrutina usando la función `async`:

```kotlin
import kotlinx.coroutines.*

fun main() {
    val deferred = async {
        // Suspend this coroutine for one second
        delay(1000)
        println("Hello, world!")
    }
    // Start the coroutine
    deferred.start()
}
```

La función `lanzamiento` es una función de suspensión, lo que significa que se puede usar dentro de otra rutina. La función `async` no es una función de suspensión, por lo que solo se puede usar desde dentro de una rutina.

## Cancelar una rutina

Las corrutinas se pueden cancelar usando la función `cancelar`. Esta función hará que la corrutina arroje una `CancellationException`.

Por ejemplo, podemos cancelar una rutina que está durmiendo por un segundo usando la función `cancelar`:

```kotlin
import kotlinx.coroutines.*

fun main() {
    val deferred = launch {
        try {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        } catch (e: CancellationException) {
            println("Coroutine was cancelled")
        }
    }
    // Cancel the coroutine after half a second
    delay(500)
    deferred.cancel()
}
```

## Tiempos de espera

Las rutinas se pueden agotar utilizando la función `withTimeout`. Esta función hará que la corrutina arroje una `TimeoutCancellationException` si no se completa dentro del tiempo especificado.

Por ejemplo, podemos agotar el tiempo de espera de una rutina que está inactiva durante un segundo usando la función `withTimeout`:

```kotlin
import kotlinx.coroutines.*

fun main() {
    try {
        withTimeout(500) {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        }
    } catch (e: TimeoutCancellationException) {
        println("Coroutine timed out")
    }
}
```

## Manejo de excepciones

Las corrutinas se pueden supervisar mediante la función `supervisorScope`. Esta función detectará cualquier excepción que arroje la rutina y continuará ejecutando el código restante.

Por ejemplo, podemos supervisar una rutina que está durmiendo durante un segundo usando la función `supervisorScope`:

```kotlin
import kotlinx.coroutines.*

fun main() {
    supervisorScope {
        val deferred = launch {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        }
        // Cancel the coroutine after half a second
        delay(500)
        deferred.cancel()
    }
}
```

## Aplicaciones web asincrónicas

Las rutinas se pueden usar para escribir aplicaciones web asincrónicas. En esta sección, veremos cómo usar rutinas en una aplicación web Java.

Comenzaremos creando un servlet simple que use una corrutina para dormir por un segundo:

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Create a new coroutine
        launch {
            // Suspend this coroutine for one second
            delay(1000)
            // Send a response to the client
            resp.getWriter().println("Hello, world!");
        }
    }
}
```

En este servlet, usamos la función `lanzar` para crear una nueva rutina. Esta rutina duerme durante un segundo y luego envía una respuesta al cliente.

También podemos usar la función `async` para crear una nueva rutina. Sin embargo, en este caso, necesitamos iniciar la rutina manualmente:

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Create a new coroutine
        val deferred = async {
            // Suspend this coroutine for one second
            delay(1000)
            // Send a response to the client
            resp.getWriter().println("Hello, world!");
        }
        // Start the coroutine
        deferred.start()
    }
}
```

En este servlet, usamos la función `async` para crear una nueva rutina. Esta rutina duerme durante un segundo y luego envía una respuesta al cliente. Usamos la función `start` para iniciar la rutina.

También es posible usar la función `withTimeout` para agotar el tiempo de espera de una rutina:

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        try {
            // Time out the coroutine after 500 milliseconds
            withTimeout(500) {
                // Create a new coroutine
                launch {
                    // Suspend this coroutine for one second
                    delay(1000)
                    // Send a response to the client
                    resp.getWriter().println("Hello, world!");
                }
            }
        } catch (e: TimeoutCancellationException) {
            // Send a timeout response to the client
            resp.getWriter().println("Request timed out");
        }
    }
}
```

En este servlet, usamos la función `withTimeout` para agotar el tiempo de espera de la corrutina. Si la rutina no se completa en 500 milisegundos, se cancelará y se enviará una respuesta de tiempo de espera al cliente.

También es posible usar la función `supervisorScope` para supervisar una rutina:

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Supervisor the coroutine
        supervisorScope {
            val deferred = launch {
                // Suspend this coroutine for one second
                delay(1000)
                // Send a response to the client
                resp.getWriter().println("Hello, world!");
            }
            // Cancel the coroutine after half a second
            delay(500)
            deferred.cancel()
        }
    }
}
```

En este servlet, usamos la función `supervisorScope` para supervisar la rutina. Esta rutina se cancela después de medio segundo, pero se ejecuta el código restante en el servlet.

## Conclusión

Las corrutinas de Kotlin brindan una forma eficiente de administrar la concurrencia en el lado del servidor. Se pueden usar con cualquier biblioteca Java existente, lo que las convierte en una gran herramienta para el desarrollo asíncrono del lado del servidor.