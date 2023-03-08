---
title: 068: Depuración de una aplicación Spring Boot con Spring Boot Debugger
description: 
published: true
date: 2023-02-05T02:17:26.809Z
tags: 
editor: markdown
dateCreated: 2023-02-05T02:17:25.187Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [068: Debugging a Spring Boot Application with the Spring Boot Debugger***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/068-debugging-a-spring-boot-application-with-the-spring-boot-debugger)
{.links-list}


# 068: Depuración de una aplicación Spring Boot con Spring Boot Debugger

Los desarrolladores enfrentan muchos desafíos cuando intentan depurar una aplicación Spring Boot. Spring Boot Debugger es una poderosa herramienta que puede ayudar a los desarrolladores a superar estos desafíos y llegar rápidamente a la raíz del problema.

En esta publicación, veremos cómo usar Spring Boot Debugger para depurar una aplicación Spring Boot. También aprenderemos sobre algunas de las funciones del depurador que se pueden usar para solucionar problemas comunes de Spring Boot.

## Configuración del depurador Spring Boot

El primer paso para usar Spring Boot Debugger es asegurarse de que esté configurado correctamente. En la mayoría de los casos, el depurador se configurará automáticamente cuando la aplicación se inicie en modo de depuración. Sin embargo, hay algunos casos en los que es posible que el depurador deba configurarse manualmente.

La forma más fácil de configurar el depurador es usar el complemento Spring Boot Debugger para su IDE. Este complemento agregará automáticamente la configuración necesaria a su aplicación.

Como alternativa, puede agregar la siguiente configuración a su archivo application.properties:

```
spring.jpa.show-sql=true
spring.h2.console.enabled=true
```

## Uso del depurador Spring Boot

Una vez que el depurador esté configurado correctamente, puede comenzar a usarlo para depurar su aplicación. El depurador se puede utilizar para depurar aplicaciones web y no web.

Para depurar una aplicación web, puede utilizar los siguientes pasos:

1. Inicie su aplicación en modo de depuración.
2. Conéctese a la aplicación mediante un cliente de depuración.
3. Establezca puntos de interrupción en su código.
4. Inspeccione las variables y analice la pila de llamadas.

Para depurar una aplicación que no es web, puede utilizar los siguientes pasos:

1. Inicie su aplicación en modo de depuración.
2. Conéctese a la aplicación mediante un cliente de depuración.
3. Establezca puntos de interrupción en su código.
4. Inspeccione las variables y analice la pila de llamadas.
5. Adjuntar a la aplicación en ejecución.

## Características del depurador Spring Boot

Spring Boot Debugger tiene muchas funciones que se pueden usar para solucionar problemas comunes de Spring Boot.

### Intercambio en caliente

Hot Swap es una función del depurador que permite a los desarrolladores realizar cambios en su código y hacer que esos cambios surtan efecto de inmediato. Esto es especialmente útil para corregir errores en una aplicación en vivo.

Para usar Hot Swap, simplemente realice los cambios deseados en su código y guarde el archivo. Los cambios entrarán en vigor inmediatamente.

### Puntos de ruptura

Los puntos de interrupción son otra característica útil del depurador. Los puntos de interrupción se pueden usar para pausar la ejecución de su código en una línea específica. Esto le permite inspeccionar las variables y la pila de llamadas para ver qué sucede en su código.

Se pueden agregar puntos de interrupción en su código haciendo clic en el número de línea en su IDE. Alternativamente, puede usar el siguiente comando para agregar un punto de interrupción:

```
debug: breakpoint MyClass.java:12
```

### Inspección de variables

Cuando su código se detiene en un punto de interrupción, puede inspeccionar los valores de las variables. Esto se puede hacer en su IDE o usando el siguiente comando:

```
debug: inspect myVariable
```

### Análisis de la pila de llamadas

La pila de llamadas se puede usar para ver la secuencia de llamadas a métodos que llevaron al estado actual de su código. Esto puede ser útil para comprender por qué su código no se comporta como se esperaba.

La pila de llamadas se puede ver en su IDE o usando el siguiente comando:

```
debug: trace
```

## Conclusión

En esta publicación, hemos visto cómo usar Spring Boot Debugger para depurar una aplicación Spring Boot. También aprendimos sobre algunas de las características del depurador que se pueden usar para solucionar problemas comunes de Spring Boot.