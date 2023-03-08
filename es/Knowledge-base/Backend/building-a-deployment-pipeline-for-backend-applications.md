---
title: Creación de una canalización de implementación para aplicaciones back-end
description: 
published: true
date: 2023-02-11T23:17:25.387Z
tags: 
editor: markdown
dateCreated: 2023-02-11T23:17:23.788Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building a Deployment Pipeline for Backend Applications***English** document is available*](/en/Knowledge-base/Backend/building-a-deployment-pipeline-for-backend-applications)
{.links-list}


# Creación de una canalización de implementación para aplicaciones back-end

En el proceso de desarrollo de software, es importante tener una estrategia sobre cómo se integran los cambios de código en una base de código y cómo se entregan esos cambios a los usuarios finales. Por lo general, esto se denomina canalización de implementación.

Una canalización de implementación para una aplicación de back-end se puede definir como una serie de pasos secuenciales que deben completarse antes de que el código se implemente en producción. Estos pasos generalmente incluyen alguna forma de prueba (por ejemplo, prueba de unidad, integración o aceptación), así como la compilación, el empaquetado y la implementación del código.

Hay muchas formas diferentes de crear una canalización de implementación y los pasos involucrados variarán según la aplicación y la infraestructura específicas. Sin embargo, hay algunos pasos comunes que normalmente se incluyen en la mayoría de las canalizaciones.

## Pasos previos a la implementación

Antes de que el código pueda implementarse en producción, primero debe pasar por una serie de pasos previos a la implementación. Estos pasos generalmente incluyen alguna forma de prueba (por ejemplo, prueba de unidad, integración o aceptación), así como la compilación, el empaquetado y la implementación del código.

### Examen de la unidad

La prueba unitaria es un tipo de prueba que aísla piezas individuales de código (generalmente clases o métodos) y las prueba de forma aislada. Esto contrasta con las pruebas de integración, que prueban cómo funcionan juntas las diferentes piezas de código.

Las pruebas unitarias generalmente las escriben los desarrolladores que escribieron el código que se está probando. Por lo general, se escriben utilizando un marco de prueba como JUnit o TestNG.

### Pruebas de integración

La prueba de integración es un tipo de prueba que prueba cómo las diferentes piezas de código funcionan juntas. Esto contrasta con la prueba unitaria, que aísla piezas individuales de código y las prueba de forma aislada.

Las pruebas de integración generalmente las escriben los desarrolladores que escribieron el código que se está probando. Por lo general, se escriben utilizando un marco de prueba como JUnit o TestNG.

### Test de aceptación

La prueba de aceptación es un tipo de prueba que se utiliza para determinar si un sistema de software cumple o no con los criterios de aceptación para una determinada parte interesada. Las pruebas de aceptación generalmente las escriben los analistas comerciales o los propietarios del producto que son responsables de los requisitos.

Por lo general, se escriben con una herramienta como Cucumber o FitNesse.

## Pasos de implementación

Una vez que el código ha superado todos los pasos previos a la implementación, está listo para implementarse en producción. Los pasos específicos involucrados en el proceso de implementación variarán según la aplicación y la infraestructura. Sin embargo, hay algunos pasos comunes que normalmente se incluyen.

### Compilando

El primer paso en el proceso de implementación es compilar el código. Este paso convierte el código fuente legible por humanos en código legible por máquina.

Los pasos específicos involucrados en la compilación del código variarán según el lenguaje de programación que se utilice. Por ejemplo, el código Java generalmente se compila con el compilador javac, mientras que el código .NET generalmente se compila con la herramienta MSBuild.

### Embalaje

El siguiente paso en el proceso de implementación es empaquetar el código. Este paso crea un artefacto implementable que se puede implementar en el entorno de destino.

Los pasos específicos involucrados en el código de empaquetado variarán según la aplicación y la infraestructura. Por ejemplo, el código Java generalmente se empaqueta con la herramienta jar, mientras que el código .NET generalmente se empaqueta con la herramienta MSBuild.

### Desplegando

El paso final en el proceso de implementación es implementar el código en el entorno de destino. Este paso generalmente implica copiar el código empaquetado en el servidor y configurar el servidor para ejecutar el código.

Los pasos específicos involucrados en la implementación del código variarán según la aplicación y la infraestructura. Por ejemplo, el código Java generalmente se implementa con el servidor web Tomcat, mientras que el código .NET generalmente se implementa con el servidor web IIS.

## Conclusión

Una canalización de implementación es una serie de pasos secuenciales que deben completarse antes de que el código se implemente en producción. Estos pasos generalmente incluyen alguna forma de prueba (por ejemplo, prueba de unidad, integración o aceptación), así como la compilación, el empaquetado y la implementación del código.

Hay muchas formas diferentes de crear una canalización de implementación y los pasos involucrados variarán según la aplicación y la infraestructura específicas. Sin embargo, hay algunos pasos comunes que normalmente se incluyen en la mayoría de las canalizaciones.