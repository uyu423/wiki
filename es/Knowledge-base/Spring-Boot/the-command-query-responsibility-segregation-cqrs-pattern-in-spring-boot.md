---
title: El patrón de segregación de responsabilidad de consulta de comando (CQRS) en Spring Boot
description: 
published: true
date: 2023-02-01T15:03:44.363Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:03:42.630Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [The Command Query Responsibility Segregation (CQRS) Pattern in Spring Boot***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/the-command-query-responsibility-segregation-cqrs-pattern-in-spring-boot)
{.links-list}


# El patrón de segregación de responsabilidad de consulta de comando (CQRS) en Spring Boot

Command Query Responsibility Segregation (CQRS) es un patrón arquitectónico que separa la responsabilidad de manejar comandos (solicitudes que cambian el estado del sistema) de la responsabilidad de manejar consultas (solicitudes que devuelven información del sistema).

Esta separación de preocupaciones puede ofrecer varios beneficios, como un mejor rendimiento, escalabilidad y mantenibilidad.

En una arquitectura CQRS, los comandos generalmente los maneja un servicio separado del que maneja las consultas. Esta separación se puede implementar de diferentes maneras, pero un enfoque común es usar diferentes tablas de base de datos para almacenar datos a los que se accede mediante comandos y datos a los que se accede mediante consultas.

Spring Boot es un marco Java popular para crear aplicaciones web. Ofrece una forma conveniente de crear aplicaciones basadas en Spring independientes y de grado de producción que se pueden "simplemente ejecutar".

En este artículo, veremos cómo implementar una arquitectura CQRS en una aplicación Spring Boot. Comenzaremos observando los diferentes componentes que están involucrados en dicha aplicación. Luego, implementaremos una aplicación de ejemplo simple que usa CQRS.

## Los componentes de una aplicación CQRS

Una aplicación CQRS normalmente tiene los siguientes componentes:

- **Comandos:** Estas son solicitudes que cambian el estado del sistema. En nuestra aplicación de ejemplo, tendremos comandos para crear y actualizar tareas.
- **Consultas:** Son solicitudes que devuelven información del sistema. En nuestra aplicación de ejemplo, tendremos consultas para obtener una lista de todas las tareas y para obtener los detalles de una tarea específica.
- **Servicio de comandos:** Este es el servicio que maneja los comandos. En nuestra aplicación de ejemplo, este servicio será el encargado de validar los comandos y ejecutarlos.
- **Servicio de consultas:** Este es el servicio que maneja las consultas. En nuestra aplicación de ejemplo, este servicio será responsable de ejecutar consultas y devolver los resultados a la persona que llama.
- **Repositorio:** Esta es una capa de acceso a datos que proporciona una interfaz para acceder al almacén de datos. En nuestra aplicación de ejemplo, usaremos un repositorio para acceder a los datos de las tareas.
- **Modelo:** Este es el modelo de dominio para la aplicación. En nuestra aplicación de ejemplo, la tarea será el único objeto modelo.


## Implementando una aplicación CQRS con Spring Boot

Ahora que hemos visto los diferentes componentes de una aplicación CQRS, implementemos una aplicación de ejemplo simple que usa CQRS.

Nuestra aplicación de ejemplo será un administrador de tareas. Los usuarios podrán crear tareas y asignárselas a sí mismos oa otros usuarios. También podrán marcar las tareas como completadas.

Comenzaremos implementando el servicio de comando. Este servicio será el encargado de validar y ejecutar comandos.

### El servicio de comando

El servicio de comando tendrá los siguientes métodos:

- **createTask(tarea de tareas)**: este método se utilizará para crear tareas.
- **updateTask(Tarea de tarea)**: Este método se utilizará para actualizar tareas.
- **markTaskAsComplete(String taskId)**: este método se utilizará para marcar las tareas como completas.

Implementaremos estos métodos en una clase llamada **TaskCommandService**. Esta clase se anotará con **@Service**, que es una anotación de Spring que marca una clase como un componente de servicio.

```java
@Service
public class TaskCommandService {

    public void createTask(Task task) {
        // validate the task
        // save the task
    }

    public void updateTask(Task task) {
        // validate the task
        // save the task
    }

    public void markTaskAsComplete(String taskId) {
        // validate the task
        // mark the task as complete
        // save the task
    }
}
```

Como puede ver, los métodos **createTask** y **updateTask** aceptan un objeto **Task** como parámetro. Este objeto se utilizará para almacenar los datos de la tarea que se está creando o actualizando.

El método **markTaskAsComplete** acepta una ID de tarea como parámetro. Este ID de tarea se usará para buscar la tarea que se marcará como completa.

Cada uno de estos métodos comienza con una llamada a un método **validar**. Este método de validación será responsable de validar los datos que se pasan. Implementaremos este método en la siguiente sección.

### Comandos de validación

El método **validar** será responsable de validar los datos que se pasan a los métodos del servicio de comando. Implementaremos este método en una clase llamada **TaskCommandValidator**. Esta clase se anotará con **@Component**, que es una anotación de Spring que marca una clase como componente.

```java
@Component
public class TaskCommandValidator {

    public void validate(Task task) {
        // validate the task
    }

    public void validate(String taskId) {
        // validate the task ID
    }
}
```

Como puede ver, esta clase tiene dos métodos de validación. Uno de estos métodos acepta un objeto **Tarea** como parámetro. Este método se utilizará para validar los datos para crear y actualizar tareas.

El otro método de validación acepta un ID de tarea como parámetro. Este método se usará para validar la identificación de la tarea para marcar tareas como completas.

En una aplicación real, estos métodos de validación contendrían lógica para validar los datos. A los efectos de este ejemplo, los dejaremos vacíos.

### El servicio de consulta

El servicio de consulta tendrá los siguientes métodos:

- **getAllTasks()**: Este método se utilizará para obtener una lista de todas las tareas.
- **getTaskById(String taskId)**: Este método se utilizará para obtener los detalles de una tarea específica.

Implementaremos estos métodos en una clase llamada **TaskQueryService**. Esta clase se anotará con **@Service**.

```java
@Service
public class TaskQueryService {

    public List<Task> getAllTasks() {
        // execute query
        // return results
    }

    public Task getTaskById(String taskId) {
        // execute query
        // return results
    }
}
```

Como puede ver, el método **getAllTasks** devuelve una lista de objetos de **Tarea**. Esta lista contendrá los datos de todas las tareas del sistema.

El método **getTaskById** devuelve un único objeto **Tarea**. Este objeto contendrá los datos de la tarea con el ID especificado.

### El repositorio

El repositorio es una capa de acceso a datos que proporciona una interfaz para acceder al almacén de datos. En nuestra aplicación de ejemplo, usaremos un repositorio para acceder a los datos de las tareas.

Implementaremos el repositorio en una clase llamada **TaskRepository**. Esta clase se anotará con **@Repository**, que es una anotación de Spring que marca una clase como un componente del repositorio.

```java
@Repository
public class TaskRepository {

    public void save(Task task) {
        // save the task
    }

    public Task findById(String id) {
        // find the task
        // return the task
    }

    public List<Task> findAll() {
        // find all tasks
        // return the tasks
    }
}
```

Como puede ver, este repositorio tiene métodos para guardar, buscar y eliminar tareas.

### El modelo

El modelo es el modelo de dominio para la aplicación. En nuestra aplicación de ejemplo, la tarea será el único objeto modelo.

Implementaremos el modelo de tarea en una clase llamada **Tarea**. Esta clase se anotará con **@Entity**, que es una anotación JPA que marca una clase como entidad.

```java
@Entity
public class Task {

    @Id
    private String id;

    private String name;

    private String description;

    private boolean complete;

    // getters and setters
}
```

Como puede ver, este modelo de tarea tiene cuatro campos: id, nombre, descripción y completo. El campo id se anota con **@Id**, que es una anotación JPA que marca un campo como la clave principal de una entidad.

### Poniendolo todo junto

Ahora que hemos implementado los diferentes componentes de nuestra aplicación CQRS, juntemos todo y veamos cómo funciona.

Comenzaremos creando una tarea. Para hacer esto, primero crearemos un objeto **Tarea** y lo completaremos con los datos de la tarea. Luego, pasaremos este objeto al método **createTask** del **TaskCommandService**.

```java
Task task = new Task();
task.setName("Write example");
task.setDescription("Write an example of the CQRS pattern");

taskCommandService.createTask(task);
```

Esto creará una nueva tarea en el sistema.

Ahora, digamos que queremos obtener una lista de todas las tareas. Para hacer esto, llamaremos al método **getAllTasks** del **TaskQueryService**.

```java
List<Task> tasks = taskQueryService.getAllTasks();
```

Esto devolverá una lista de todas las tareas en el sistema.

Finalmente, digamos que queremos marcar una tarea como completa. Para hacer esto, primero obtendremos la tarea por ID. Luego, llamaremos al método **markTaskAsComplete** del **TaskCommandService**.

```java
Task task = taskQueryService.getTaskById("1");

taskCommandService.markTaskAsComplete(task.getId());
```

Esto marcará la tarea con ID "1" como completa.

## Conclusión

En este artículo, analizamos el patrón Command Query Responsibility Segregation (CQRS) y cómo se puede implementar en una aplicación Spring Boot.

También hemos visto cómo este patrón puede ofrecer varios beneficios, como un mejor rendimiento, escalabilidad y facilidad de mantenimiento.

Si está interesado en obtener más información sobre CQRS, le recomiendo los siguientes recursos:

- [CQRS: Lo bueno, lo malo y lo feo](https://martinfowler.com/bliki/CQRS.html)
- [Segregación de responsabilidad de consulta de comando] (https://en.wikipedia.org/wiki/Command%E2%80%93query_separation)
- [¿Por qué usar CQRS?](https://docs.microsoft.com/en-us/azure/architecture/patterns/cqrs)