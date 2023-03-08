---
title: Trabajar con la interfaz de herramienta de máquina virtual de Java (JVMTI)
description: 
published: true
date: 2023-02-16T18:55:48.146Z
tags: 
editor: markdown
dateCreated: 2023-02-16T18:55:40.359Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with the Java Virtual Machine Tool Interface (JVMTI)***English** document is available*](/en/Knowledge-base/Java/working-with-the-java-virtual-machine-tool-interface-jvmti)
{.links-list}


# Trabajar con la interfaz de herramienta de máquina virtual de Java (JVMTI)

La interfaz de herramienta de máquina virtual de Java (JVMTI) es una interfaz de programación utilizada por las herramientas de desarrollo para obtener información sobre el estado de ejecución de una máquina virtual de Java (JVM). También brinda la capacidad de manipular el estado de la JVM, como suspender y reanudar subprocesos, establecer puntos de interrupción y obtener y establecer variables locales.

## Obtención de información JVMTI

La información de JVMTI se puede dividir en dos categorías: información sobre la propia JVM e información sobre los subprocesos y métodos que se ejecutan dentro de la JVM.

La información sobre la propia JVM se puede obtener a través de la estructura del entorno JVMTI. Esta estructura contiene una serie de funciones que se pueden usar para consultar las capacidades de la JVM, el uso de la memoria, el estado del recolector de elementos no utilizados y más.

La información sobre subprocesos y métodos que se ejecutan dentro de la JVM se puede obtener a través de las estructuras JVMTI Thread y JVMTI Method. Estas estructuras contienen una serie de funciones que se pueden usar para consultar el estado actual de un subproceso o método, como el seguimiento de la pila, las variables locales y el número de línea.

## Manipulación del estado de la JVM

La JVMTI proporciona una serie de funciones para manipular el estado de la JVM. Estas funciones se pueden usar para suspender y reanudar subprocesos, establecer puntos de interrupción y obtener y establecer variables locales.

## Suspender y reanudar hilos

La JVMTI proporciona funciones para suspender y reanudar subprocesos. Estas funciones se pueden usar para detener temporalmente la ejecución de un subproceso o para evitar que se inicie un subproceso.

El siguiente ejemplo de código muestra cómo usar JVMTI para suspender un hilo:

```
jvmtiEnv* jvmti;
jvmtiError error;

// Get the JVMTI environment
error = (*jvmti)->GetEnv(jvmti, &jvmti, JVMTI_VERSION_1);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}

// Suspend the thread
error = (*jvmti)->SuspendThread(jvmti, thread);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}
```

## Establecer puntos de interrupción

El JVMTI proporciona funciones para establecer puntos de interrupción. Estas funciones se pueden usar para establecer un punto de interrupción en una línea de código específica o en un método específico.

El siguiente ejemplo de código muestra cómo utilizar JVMTI para establecer un punto de interrupción en una línea de código específica:

```
jvmtiEnv* jvmti;
jvmtiError error;

// Get the JVMTI environment
error = (*jvmti)->GetEnv(jvmti, &jvmti, JVMTI_VERSION_1);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}

// Set the breakpoint
error = (*jvmti)->SetBreakpoint(jvmti, method, line_number);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}
```

## Obtención y configuración de variables locales

El JVMTI proporciona funciones para obtener y establecer variables locales. Estas funciones se pueden utilizar para inspeccionar el valor de una variable local o para cambiar el valor de una variable local.

El siguiente ejemplo de código muestra cómo usar JVMTI para obtener el valor de una variable local:

```
jvmtiEnv* jvmti;
jvmtiError error;

// Get the JVMTI environment
error = (*jvmti)->GetEnv(jvmti, &jvmti, JVMTI_VERSION_1);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}

// Get the value of the local variable
error = (*jvmti)->GetLocalVariable(jvmti, thread, method,
                                   local_variable, &value);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}
```

El siguiente ejemplo de código muestra cómo usar JVMTI para establecer el valor de una variable local:

```
jvmtiEnv* jvmti;
jvmtiError error;

// Get the JVMTI environment
error = (*jvmti)->GetEnv(jvmti, &jvmti, JVMTI_VERSION_1);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}

// Set the value of the local variable
error = (*jvmti)->SetLocalVariable(jvmti, thread, method,
                                   local_variable, value);
if (error != JVMTI_ERROR_NONE) {
    // Handle error
}
```

## Conclusión

La interfaz de herramienta de máquina virtual de Java (JVMTI) es una interfaz de programación poderosa que se puede utilizar para obtener información sobre el estado de ejecución de una máquina virtual de Java (JVM). También brinda la capacidad de manipular el estado de la JVM, como suspender y reanudar subprocesos, establecer puntos de interrupción y obtener y establecer variables locales.