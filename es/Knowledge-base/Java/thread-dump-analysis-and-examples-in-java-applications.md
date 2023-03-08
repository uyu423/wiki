---
title: Análisis de volcado de subprocesos y ejemplos en aplicaciones Java
description: 
published: true
date: 2023-02-09T02:49:44.424Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:49:42.822Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Thread Dump Analysis and Examples in Java Applications***English** document is available*](/en/Knowledge-base/Java/thread-dump-analysis-and-examples-in-java-applications)
{.links-list}


# Análisis de volcado de subprocesos y ejemplos en aplicaciones Java

Los volcados de subprocesos son una herramienta valiosa para diagnosticar problemas de rendimiento en aplicaciones Java. En este artículo, veremos qué son los volcados de subprocesos, cómo generarlos y cómo analizarlos. También proporcionaremos algunos ejemplos de cómo se pueden usar los volcados de subprocesos para solucionar problemas comunes de rendimiento de Java.

## ¿Qué es un volcado de subprocesos?

Un volcado de subprocesos es una instantánea del estado de todos los subprocesos en un proceso Java. Los volcados de subprocesos pueden ser útiles para diagnosticar problemas de rendimiento, interbloqueos y otros problemas.

## Cómo generar un volcado de subprocesos

Hay algunas formas diferentes de generar un volcado de subprocesos.

### jstack

La herramienta jstack está incluida en el JDK y se puede utilizar para generar un volcado de subprocesos para un proceso Java en ejecución. Para usar jstack, simplemente especifique el ID del proceso Java para el que desea generar un volcado de subprocesos. Por ejemplo:

```
jstack 12345
```

### jcmd

La herramienta jcmd también se incluye en el JDK y se puede utilizar para generar un volcado de subprocesos para un proceso Java en ejecución. Para usar jcmd, simplemente especifique el ID de proceso del proceso Java para el que desea generar un volcado de subprocesos. Por ejemplo:

```
jcmd 12345 Thread.print
```

### IDE

Algunos IDE, como Eclipse e IntelliJ IDEA, tienen compatibilidad integrada para generar volcados de subprocesos. Por ejemplo, en Eclipse, puede generar un volcado de hilo yendo a **Ventana** > **Mostrar vista** > **Otro** > **Depurar** > **Subprocesos**. Luego, seleccione el proceso Java para el que desea generar un volcado de subprocesos y haga clic en el botón **Volcar subprocesos**.

## Cómo analizar un volcado de subprocesos

Una vez que tenga un volcado de subprocesos, puede usar una herramienta como jstackAnalyzer o VisualVM para visualizarlo. Como alternativa, puede analizar el volcado de subprocesos manualmente.

Al analizar un volcado de subprocesos, busca dos cosas:

1. Subprocesos que se encuentran en un estado "ejecutable". Estos son los hilos que están trabajando actualmente.
2. Subprocesos que están en estado de "espera". Estos son los subprocesos que están esperando que otros subprocesos funcionen.

Si ve muchos subprocesos en un estado de "espera", eso suele ser una indicación de que hay un problema de rendimiento. Por ejemplo, si hay muchos subprocesos esperando una conexión a la base de datos, eso podría ser una indicación de que la base de datos es lenta.

Si ve muchos subprocesos en un estado "ejecutable", eso suele ser una indicación de que hay un cuello de botella en la CPU.

## Ejemplos

Estos son algunos ejemplos de cómo se pueden usar los volcados de subprocesos para solucionar problemas comunes de rendimiento de Java.

### punto muerto

Un interbloqueo es una situación en la que dos o más subprocesos están bloqueados esperando que el otro funcione. Esto puede suceder, por ejemplo, si el subproceso A está esperando que el subproceso B funcione y el subproceso B está esperando que el subproceso A funcione.

Aquí hay un ejemplo de un interbloqueo de un volcado de subprocesos:

```
"Thread-1" #11 prio=5 os_prio=0 tid=0x000000000019f800 nid=0xb34 waiting for monitor entry [0x00000000001b2000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at Deadlock.run(Deadlock.java:22)
	- waiting to lock <0x00000000d7216928> (a java.lang.String)
	- locked <0x00000000d7216940> (a java.lang.String)

"Thread-0" #10 prio=5 os_prio=0 tid=0x000000000019e800 nid=0x5bc waiting for monitor entry [0x00000000001a2000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at Deadlock.run(Deadlock.java:17)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)
```

En este volcado de subprocesos, podemos ver que Subproceso-1 está esperando que Subproceso-0 funcione, y Subproceso-0 está esperando que Subproceso-1 funcione. Este es un punto muerto.

Para solucionar un interbloqueo, debe identificar los subprocesos que están involucrados en el interbloqueo y averiguar qué están esperando. En este ejemplo, Thread-1 está esperando que Thread-0 funcione y Thread-0 está esperando que Thread-1 funcione. Para solucionar esto, debe asegurarse de que Thread-0 haga su trabajo antes que Thread-1, o viceversa.

### Cuello de botella de la CPU

Un cuello de botella en la CPU es una situación en la que la CPU está sobrecargada y no puede satisfacer la demanda. Esto puede suceder, por ejemplo, si hay demasiados subprocesos ejecutándose al mismo tiempo.

Aquí hay un ejemplo de un cuello de botella de CPU de un volcado de subprocesos:

```
"Thread-0" #10 prio=5 os_prio=0 tid=0x000000000019e800 nid=0x5bc runnable [0x00000000001a2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-1" #11 prio=5 os_prio=0 tid=0x000000000019f800 nid=0xb34 runnable [0x00000000001b2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-2" #12 prio=5 os_prio=0 tid=0x00000000001a0800 nid=0x1424 runnable [0x00000000001c2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-3" #13 prio=5 os_prio=0 tid=0x00000000001a1800 nid=0xd74 runnable [0x00000000001d2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-4" #14 prio=5 os_prio=0 tid=0x00000000001a2800 nid=0x1238 runnable [0x00000000001e2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-5" #15 prio=5 os_prio=0 tid=0x00000000001a3800 nid=0x1a8 runnable [0x00000000001f2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-6" #16 prio=5 os_prio=0 tid=0x00000000001a4800 nid=0x1658 runnable [0x0000000000202000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-7" #17 prio=5 os_prio=0 tid=0x00000000001a5800 nid=0x6e4 runnable [0x0000000000212000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-8" #18 prio=5 os_prio=0 tid=0x00000000001a6800 nid=0x1740 runnable [0x0000000000222000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-9" #19 prio=5 os_prio=0 tid=0x00000000001a7800 nid=0x15fc runnable [0x0000000000232000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)
```

En este volcado de subprocesos, podemos ver que hay 10 subprocesos ejecutándose al mismo tiempo. Esto está causando un cuello de botella en la CPU.

Para solucionar un cuello de botella de la CPU, debe identificar los subprocesos que causan el problema y descubrir por qué se ejecutan tanto. En este ejemplo, los subprocesos ejecutan un bucle ocupado. Para solucionar esto, debe asegurarse de que los subprocesos no ejecuten el bucle ocupado durante más tiempo del necesario.

### Cuello de botella en la base de datos

Un cuello de botella en la base de datos es una situación en la que la base de datos es lenta y no puede satisfacer la demanda. Esto puede suceder, por ejemplo, si hay demasiadas consultas a la base de datos.

Aquí hay un ejemplo de un cuello de botella en la base de datos de un volcado de subprocesos:

```
"Thread-0" #10 prio=5 os_prio=0 tid=0x000000000019e800 nid=0x5bc waiting for monitor entry [0x00000000001a2000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at Deadlock.run(Deadlock.java:17)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-1" #11 prio=5 os_prio=0 tid=0x000000000019f800 nid=0xb34 runnable [0x00000000001b2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-2" #12 prio=5 os_prio=0 tid=0x00000000001a0800 nid=0x1424 runnable [0x00000000001c2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-3" #13 prio=5 os_prio=0 tid=0x00000000001a1800 nid=0xd74 runnable [0x00000000001d2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-4" #14 prio=5 os_prio=0 tid=0x00000000001a2800 nid=0x1238 runnable [0x00000000001e2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-5" #15 prio=5 os_prio=0 tid=0x00000000001a3800 nid=0x1a8 runnable [0x00000000001f2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-6" #16 prio=5 os_prio=0 tid=0x00000000001a4800 nid=0x1658 waiting for monitor entry [0x0000000000202000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-7" #17 prio=5 os_prio=0 tid=0x00000000001a5800 nid=0x6e4 waiting for monitor entry [0x0000000000212000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-8" #18 prio=5 os_prio=0 tid=0x00000000001a6800 nid=0x1740 waiting for monitor entry [0x0000000000222000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-9" #19 prio=5 os_prio=0 tid=0x00000000001a7800 nid=0x15fc waiting for monitor entry [0x0000000000232000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)
```

En este volcado de subprocesos, podemos ver que hay 10 subprocesos ejecutándose al mismo tiempo, todos los cuales están esperando que la base de datos funcione. Esto está causando un cuello de botella en la base de datos.

Para solucionar un cuello de botella en la base de datos, debe identificar los subprocesos que causan el problema y averiguar por qué están esperando la base de datos. En este ejemplo, los subprocesos ejecutan una consulta que tarda mucho tiempo en ejecutarse. Para solucionar esto, debe optimizar la consulta.

## Conclusión

Los volcados de subprocesos son una herramienta valiosa para diagnosticar problemas de rendimiento en aplicaciones Java. En este artículo, hemos analizado qué son los volcados de subprocesos, cómo generarlos y cómo analizarlos. También proporcionamos algunos ejemplos de cómo se pueden usar los volcados de subprocesos para solucionar problemas comunes de rendimiento de Java.