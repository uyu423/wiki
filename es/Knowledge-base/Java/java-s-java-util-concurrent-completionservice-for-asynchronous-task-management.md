---
title: java.util.concurrent.CompletionService de Java para la gestión de tareas asincrónicas
description: 
published: true
date: 2023-02-03T22:55:16.447Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:55:11.468Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's java.util.concurrent.CompletionService for Asynchronous Task Management***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-completionservice-for-asynchronous-task-management)
{.links-list}


# java.util.concurrent.CompletionService de Java para la gestión de tareas asincrónicas

`java.util.concurrent.CompletionService` de Java es una poderosa herramienta para administrar tareas asincrónicas. Le permite enviar tareas y realizar un seguimiento de su progreso, recibir notificaciones cuando se completan las tareas e incluso cancelar tareas si es necesario.

Aquí hay un ejemplo simple de cómo usar `CompletionService` para enviar una tarea y seguir su progreso:

```java
// Create a CompletionService
CompletionService<String> service = new ExecutorCompletionService<>(executor);

// Submit a task
Future<String> future = service.submit(new Callable<String>() {
    @Override
    public String call() throws Exception {
        // Do some work
        return "Result";
    }
});

// Track the task's progress
while (!future.isDone()) {
    // Do something else
}

// Get the task's result
String result = future.get();
```

Como puede ver, `CompletionService` facilita el envío y el seguimiento del progreso de las tareas asincrónicas. También proporciona métodos convenientes para recibir notificaciones cuando se completan las tareas y para cancelar tareas si es necesario.

Recursos externos:

- [JavaDoc para CompletionService](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletionService.html)
- [Tutorial de simultaneidad de Java: CompletionService](https://www.baeldung.com/java-completion-service)
- [Consejo de Java 67: use el servicio de finalización de Java] (https://www.javaworld.com/article/2077322/java-tip-67--use-the-java-completion-service.html)