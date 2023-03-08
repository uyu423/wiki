---
title: java.util.concurrent.locks.ReentrantLock de Java para bloqueo reentrante
description: 
published: true
date: 2023-02-12T02:55:26.670Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:55:25.085Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's java.util.concurrent.locks.ReentrantLock for Reentrant Locking***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-locks-reentrantlock-for-reentrant-locking)
{.links-list}


# java.util.concurrent.locks.ReentrantLock de Java para bloqueo reentrante

El bloqueo de reentrada es un mecanismo popular para garantizar la seguridad de subprocesos en aplicaciones Java. En este artículo, veremos de cerca cómo funciona ReentrantLock en Java.

ReentrantLock es parte de las utilidades de concurrencia de Java e implementa la interfaz Lock. Proporciona un mecanismo de bloqueo más sofisticado que los bloqueos intrínsecos disponibles en Java.

Política de equidad de ReentrantLock

Hay dos tipos de política de equidad para ReentrantLock:

* Justo
* No justo

La política justa evita que los subprocesos mueran de hambre mientras esperan el bloqueo. En un ReentrantLock justo, cuando varios subprocesos están esperando el bloqueo, el subproceso que ha estado esperando más tiempo recibe el bloqueo primero.

La política no justa es la política predeterminada y no ofrece ninguna garantía sobre el orden en que los subprocesos adquieren el bloqueo. Esta política es más eficiente que la política justa.

Cómo funciona ReentrantLock

ReentrantLock usa un objeto de bloqueo interno para representar el estado bloqueado. Cuando un subproceso invoca el método lock(), adquiere el bloqueo si está disponible. Si el bloqueo no está disponible, el subproceso entra en un estado de espera.

Cuando un subproceso adquiere un bloqueo, obtiene un recuento de espera. El subproceso puede liberar el bloqueo invocando el método unlock(). El bloqueo se libera solo cuando el recuento de espera del subproceso llega a cero.

Si un subproceso intenta adquirir un bloqueo que ya tiene, se incrementa el número de retenciones del subproceso.

Un subproceso puede liberar un bloqueo que no tiene invocando el método unlock(). Esto da como resultado una IllegalMonitorStateException.

El método tryLock()

El método tryLock() se usa para adquirir un bloqueo. Si el bloqueo está disponible, el subproceso adquiere el bloqueo y el método devuelve verdadero. Si el bloqueo no está disponible, el subproceso no se bloquea y el método devuelve falso.

El método tryLock(long time, TimeUnit unit) se usa para adquirir un bloqueo dentro de un tiempo específico. Si el bloqueo está disponible, el subproceso adquiere el bloqueo y el método devuelve verdadero. Si el bloqueo no está disponible, el subproceso se bloquea hasta que expire el tiempo especificado. Si el tiempo expira antes de que el bloqueo esté disponible, el subproceso no adquiere el bloqueo y el método devuelve falso.

El método lockInterruptably()

El método lockInterruptably() se utiliza para adquirir un bloqueo. Si el bloqueo está disponible, el subproceso adquiere el bloqueo. Si el bloqueo no está disponible, el subproceso se bloquea hasta que el bloqueo esté disponible o se interrumpa el subproceso.

El método nuevaCondición()

El método newCondition() crea un nuevo objeto Condition que está vinculado a esta instancia de Lock.

El método isHeldByCurrentThread()

El método isHeldByCurrentThread() devuelve verdadero si el subproceso actual mantiene este bloqueo y falso en caso contrario.

El método isLocked()

El método isLocked() devuelve verdadero si este bloqueo está retenido por cualquier subproceso y falso en caso contrario.

El método getQueueLength()

El método getQueueLength() devuelve el número de subprocesos que esperan para adquirir este bloqueo.

El método hasQueuedThreads()

El método hasQueuedThreads() devuelve verdadero si hay subprocesos esperando para adquirir este bloqueo y falso en caso contrario.

El método isFair()

El método isFair() devuelve verdadero si este bloqueo es justo y falso en caso contrario.

El método getHoldCount()

El método getHoldCount() devuelve el número de bloqueos retenidos por el subproceso actual.

El método toString()

El método toString() devuelve una representación de cadena de este bloqueo.