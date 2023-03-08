---
title: El patrón observador en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-08T13:32:49.732Z
tags: 
editor: markdown
dateCreated: 2023-02-08T13:32:47.577Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Observer Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-observer-pattern-in-spring-boot-development)
{.links-list}


# El patrón Observer en el desarrollo de Spring Boot

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

Es un patrón muy útil para la programación basada en eventos y es uno de los cimientos del patrón arquitectónico Model-View-Controller (MVC).

En este artículo, veremos cómo usar el patrón Observer en una aplicación Spring Boot. Comenzaremos analizando los conceptos básicos del patrón y cómo se usa normalmente. Luego veremos cómo Spring Boot facilita la implementación del patrón con su soporte integrado para la especificación JavaBeans.

## ¿Qué es el patrón del observador?

Como mencionamos, Observer Pattern es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente sobre cualquier cambio de estado, generalmente llamando a uno de sus métodos.

Hay algunas cosas a tener en cuenta sobre esta definición:

- El sujeto es un objeto, no una clase. Esto significa que un sujeto puede ser cualquier tipo de objeto, incluido un tipo primitivo como un int o un String.

- Los observadores también son objetos, no clases. Esto significa que un observador puede ser cualquier tipo de objeto, incluido un tipo primitivo como un int o un String.

- El sujeto mantiene una lista de sus observadores. Esta lista normalmente se implementa como una colección, como ArrayList o LinkedList.

- El sujeto notifica a sus observadores llamando a uno de sus métodos. El método al que se llama depende de la implementación, pero normalmente es un método que es específico del patrón Observer, como update() o handleEvent().

- El patrón de observador se usa a menudo en la programación basada en eventos. Esto significa que los observadores son notificados de los cambios de estado en el sujeto a medida que ocurren, en lugar de ser encuestados por cambios.

Ahora que hemos visto los conceptos básicos del patrón de observador, echemos un vistazo a cómo se usa normalmente.

## ¿Cómo se usa el patrón del observador?

Hay algunas formas diferentes en las que se puede usar el patrón de observador, pero la más común es en la programación basada en eventos.

En la programación dirigida por eventos, la aplicación generalmente se organiza en torno a un bucle de eventos central. Los eventos son generados por el usuario, por el hardware o por la propia aplicación, y son manejados por controladores de eventos.

El patrón de observador se puede utilizar para desacoplar los controladores de eventos del bucle de eventos. Los controladores de eventos se pueden implementar como observadores y se pueden registrar con el bucle de eventos. Cuando ocurre un evento, el bucle de eventos notifica a los observadores y pueden manejar el evento.

Esto tiene algunas ventajas:

- Los controladores de eventos se pueden implementar como componentes reutilizables.

- Los controladores de eventos se pueden registrar y desregistrar en tiempo de ejecución.

- Los controladores de eventos se pueden llamar en cualquier orden.

- Los controladores de eventos se pueden llamar simultáneamente.

Veamos cómo usar el patrón Observer en una aplicación Spring Boot.

## Uso del patrón de observador en Spring Boot

Spring Boot facilita el uso de Observer Pattern con su soporte integrado para la especificación JavaBeans.

JavaBeans es una especificación para componentes Java que define un conjunto de convenciones para escribir código Java. Una de las convenciones es que un componente JavaBeans debe tener un método setter al estilo JavaBeans para cada una de sus propiedades.

Por ejemplo, si un componente tiene una propiedad llamada foo, el componente debe tener un método setFoo(). Cuando se llama al método setFoo(), el componente debe activar un FooPropertyChangeEvent.

Spring Boot usa esta convención para admitir el patrón Observer. Cuando se inicia una aplicación Spring Boot, escanea el classpath en busca de clases que tengan métodos setter de estilo JavaBeans. Para cada método setter, registra un observador.

Cuando se llama al método setter, se notifica al observador. El observador puede entonces tomar cualquier acción que sea apropiada, como llamar a un método sobre el tema o registrar un mensaje.

Veamos cómo funciona esto con un ejemplo simple.

## Ejemplo

Considere una aplicación Spring Boot que tiene una propiedad llamada foo. La aplicación establece la propiedad foo en el archivo application.properties:

foo=barra

La aplicación también tiene una clase llamada FooObserver que implementa la interfaz Observer:

FooObserver de clase pública implementa Observer {

    @Anular
    actualización de vacío público (observable o, objeto arg) {
        // hacer algo
    }

}

Cuando se inicia la aplicación, el marco Spring Boot escanea el classpath en busca de clases que tengan métodos setter de estilo JavaBeans. Encuentra la clase FooObserver y la registra como observador de la propiedad foo.

Cuando la aplicación establece la propiedad foo, el marco Spring Boot llama al método update() de FooObserver. El método update() puede entonces tomar cualquier acción que sea apropiada, como registrar un mensaje o llamar a un método sobre el asunto.

Este ejemplo muestra cómo se puede usar el patrón Observer para desacoplar los componentes de una aplicación Spring Boot. Los observadores se pueden implementar como componentes reutilizables y se pueden registrar y desregistrar en tiempo de ejecución.

## Conclusión

En este artículo, hemos visto cómo usar el patrón Observer en una aplicación Spring Boot. Hemos analizado los conceptos básicos del patrón y cómo se usa normalmente. Luego, hemos visto cómo Spring Boot facilita la implementación del patrón con su soporte integrado para la especificación JavaBeans.