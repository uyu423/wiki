---
title: Paquete java.nio de Java para operaciones de E/S sin bloqueo
description: 
published: true
date: 2023-02-15T11:17:45.052Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:17:43.330Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's java.nio Package for Non-Blocking I/O Operations***English** document is available*](/en/Knowledge-base/Java/java-s-java-nio-package-for-non-blocking-io-operations)
{.links-list}



# Paquete java.nio de Java para operaciones de E/S sin bloqueo

El paquete `java.nio` de Java proporciona API para realizar operaciones de entrada/salida (E/S) *sin bloqueo* en Java. La E/S sin bloqueo significa que un subproceso puede iniciar una operación de E/S sin tener que esperar a que se complete la operación. Esto puede conducir a operaciones de E/S más eficientes, ya que un subproceso puede realizar otro trabajo mientras se realiza la operación de E/S.

## Descripción general de java.nio

El paquete `java.nio` se introdujo en Java 1.4 y proporciona lo siguiente:

- Un conjunto de clases `Buffer` para almacenar datos en varios tipos primitivos
- Un conjunto de clases `Channel` para realizar operaciones de E/S
- Un conjunto de clases `Selector` para multiplexar operaciones de E/S
- Un conjunto de clases `FileLock` y `FileChannel` para realizar operaciones de E/S basadas en archivos

Además, el paquete `java.nio.file` se introdujo en Java 7 y brinda soporte para operaciones de E/S basadas en archivos.

## Buffer

Un `Buffer` es un contenedor de datos de un tipo primitivo específico. Hay clases `Buffer` para cada uno de los tipos de datos primitivos: `ByteBuffer`, `CharBuffer`, `DoubleBuffer`, `FloatBuffer`, `IntBuffer`, `LongBuffer` y `ShortBuffer`.

Un `Buffer` tiene las siguientes propiedades:

- **Capacidad:** El número máximo de elementos que se pueden almacenar en el búfer.
- **Límite:** El índice del primer elemento que no se debe leer ni escribir.
- **Posición:** El índice del siguiente elemento que se leerá o escribirá.

Un `Buffer` también tiene los siguientes métodos:

- `clear()`: Establece la posición a 0 y el límite a la capacidad.
- `flip()`: Establece el límite a la posición actual y la posición a 0.
- `rewind()`: establece la posición en 0.
- `remaining()`: Devuelve el número de elementos entre la posición y el límite.
- `hasRemaining()`: Devuelve `true` si quedan elementos, `false` en caso contrario.

## Canal

Un 'Channel' es una estructura similar a un 'Búfer' que representa una conexión abierta a un dispositivo de E/S. Un 'Canal' puede estar abierto para lectura, escritura o ambos.

Hay varios tipos de `Channel`s, incluidos `FileChannel`, `DatagramChannel`, `SocketChannel` y `Pipe.SinkChannel`.

Un `Channel` tiene los siguientes métodos:

- `isOpen()`: Devuelve `verdadero` si el canal está abierto, `falso` en caso contrario.
- `close()`: Cierra el canal.
- `read(Buffer)`: Lee datos del canal en el búfer dado.
- `write(Buffer)`: escribe datos del búfer dado en el canal.

## Selector

Se utiliza un `Selector` para multiplexar operaciones de E/S. Se puede usar un `Selector` para esperar a que se completen las operaciones de E/S en uno o más `Channel`s.

Un `Selector` tiene los siguientes métodos:

- `open()`: Abre un `Selector`.
- `close()`: Cierra el `Selector`.
- `select()`: Devuelve las `SelectionKey`s para los `Channel`s en los que las operaciones de E/S están listas para realizarse.
- `select(long)`: Devuelve las `SelectionKey`s para los `Channel`s en los que las operaciones de E/S están listas para realizarse, o `null` si el tiempo de espera expira.
- `selectedKeys()`: Devuelve el `Conjunto` de `SelectionKey`s para el `Channel`s en el que las operaciones de E/S están listas para realizarse.
- `keys()`: Devuelve el `Conjunto` de `SelectionKey`s para todos los `Channel`s registrados con este `Selector`.

## Bloqueo de archivo

Un `FileLock` se usa para bloquear una región de un `FileChannel`. Un `FileLock` tiene los siguientes métodos:

- `isShared()`: Devuelve `verdadero` si el bloqueo es compartido, `falso` en caso contrario.
- `release()`: Libera el bloqueo.
- `isValid()`: devuelve `verdadero` si el bloqueo aún es válido, `falso` en caso contrario.

## Canal de archivo

Un `FileChannel` es un `Channel` que se utiliza para realizar operaciones de E/S basadas en archivos. Un `FileChannel` tiene los siguientes métodos:

- `lock(long, long, boolean)`: Bloquea una región del archivo.
- `tryLock()`: intenta bloquear una región del archivo.
- `read(ByteBuffer, long)`: Lee datos del archivo en el búfer dado.
- `write(ByteBuffer, long)`: escribe datos del búfer dado en el archivo.

## java.nio.archivo

El paquete `java.nio.file` se introdujo en Java 7 y brinda soporte para operaciones de E/S basadas en archivos. Este paquete contiene las siguientes clases:

- `Ruta`: una representación de una ruta del sistema de archivos.
- `Paths`: Una fábrica para crear objetos `Path`.
- `Files`: una clase de utilidad para realizar operaciones relacionadas con archivos.

## Conclusión

El paquete `java.nio` de Java proporciona API para realizar operaciones de E/S sin bloqueo en Java. El paquete `java.nio.file` se introdujo en Java 7 y brinda soporte para operaciones de E/S basadas en archivos.