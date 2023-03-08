---
title: Programación orientada a aspectos con Spring AOP
description: 
published: true
date: 2023-02-07T00:32:34.317Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:32:32.684Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Aspect-Oriented Programming with Spring AOP***English** document is available*](/en/Knowledge-base/Spring-Boot/aspect-oriented-programming-with-spring-aop)
{.links-list}


# Programación orientada a aspectos con Spring AOP

La programación orientada a aspectos (AOP) es un paradigma de programación que tiene como objetivo aumentar la modularidad al permitir la separación de preocupaciones transversales. AOP forma la base de los marcos de aplicaciones empresariales como Spring AOP.

Spring AOP es una poderosa herramienta para la programación orientada a aspectos en Java. Le permite modularizar preocupaciones transversales en aspectos separados y aplicarlos a beans implementados en un contexto de aplicación Spring. En este artículo, veremos cómo usar Spring AOP para implementar casos de uso comunes de AOP, como el registro, la auditoría y la supervisión del rendimiento.

Comenzaremos con un ejemplo simple de cómo usar Spring AOP para registrar el tiempo de ejecución del método. Luego veremos cómo usar puntos de corte y consejos para aplicar aspectos a beans en un contexto de aplicación Spring.

## Tiempo de ejecución del método de registro

Supongamos que tenemos un servicio simple que queremos registrar el tiempo de ejecución de cada método:

```java
public class MyService {

    public void doWork() {
        // do some work
    }
}
```

Podemos usar Spring AOP para registrar el tiempo de ejecución de cada método en este servicio con el siguiente aspecto:

```java
@Aspect
@Component
public class LoggingAspect {

    @Around("execution(* com.example.myservice.*.*(..))")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        Object proceed = joinPoint.proceed();
        long elapsedTime = System.currentTimeMillis() - start;
        System.out.println(joinPoint.getSignature() + " executed in " + elapsedTime + "ms");
        return proceed;
    }
}
```

La anotación `@Around` indica que se trata de un consejo de alrededor. La expresión pointcut `execution(* com.example.myservice.*.*(..))` le dice a Spring AOP que aplique este aspecto a todos los métodos en el paquete `com.example.myservice`.

El método `logExecutionTime()` es el consejo real. Toma un `ProceedingJoinPoint` como argumento, que representa el método recomendado. El método `logExecutionTime()` primero obtiene el tiempo actual en milisegundos, luego llama al método `proceed()` en el punto de unión para ejecutar el método recomendado y finalmente calcula el tiempo transcurrido y lo imprime en la consola.

Para aplicar este aspecto a nuestra clase `MyService`, necesitamos agregar la anotación `@EnableAspectJAutoProxy` a nuestra configuración:

```java
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyService();
    }

    @Bean
    public LoggingAspect loggingAspect() {
        return new LoggingAspect();
    }
}
```

La anotación `@EnableAspectJAutoProxy` habilita el mecanismo de auto-proxy de Spring, que procesa beans con aspectos para que los aspectos se apliquen a ellos.

Entonces podemos usar el bean `MyService` en nuestra aplicación:

```java
public class App {

    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        MyService myService = context.getBean(MyService.class);
        myService.doWork();
    }
}
```

Cuando ejecutamos esta aplicación, vemos el siguiente resultado:

```
void com.example.myservice.MyService.doWork() executed in 0ms
```

También podemos usar el consejo `@Around` para implementar otros casos de uso de AOP, como la auditoría y la supervisión del rendimiento.

## Aplicando Aspectos a los Frijoles

En la sección anterior, vimos cómo usar el consejo `@Around` para registrar el tiempo de ejecución del método. Pero, ¿y si queremos aplicar este aspecto solo a algunos de los beans de nuestra aplicación? Podemos hacer esto usando puntos de corte y consejos.

Un punto de corte es un predicado que coincide con los puntos de unión. Un punto de unión es un punto en la ejecución de un programa donde se puede conectar un aspecto. En Spring AOP, un punto de unión siempre representa una invocación de método.

Un consejo está asociado con un punto de corte y se ejecuta cuando se alcanza un punto de unión que coincide con el punto de corte. Hay cuatro tipos de consejos en Spring AOP:

- `@Before`: ejecutado antes del punto de unión
- `@After`: ejecutado después del punto de unión, ya sea que arroje o no una excepción
- `@AfterReturning`: ejecutado después de que el punto de unión se complete normalmente
- `@AfterThrowing`: ejecutado después de que el punto de unión arroja una excepción

Podemos usar cortes de puntos y consejos para aplicar selectivamente aspectos a los beans en nuestra aplicación. Por ejemplo, supongamos que queremos aplicar `LoggingAspect` solo a beans cuyos nombres comienzan con `myService`. Esto lo podemos hacer con la siguiente configuración:

```java
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

    @Bean
    @Lazy
    @Scope("prototype")
    @Pointcut("bean(*myService*)")
    public LoggingAspect loggingAspect() {
        return new LoggingAspect();
    }
}
```

Aquí hemos anotado el método `loggingAspect()` con `@Pointcut`, que le dice a Spring AOP que aplique este aspecto a todos los beans cuyos nombres comienzan con `myService`. También hemos anotado el bean de aspecto con `@Lazy` y `@Scope("prototype")` para garantizar que el aspecto se aplique solo a los beans que están instanciados por el contexto de la aplicación.

Con esta configuración en su lugar, `LoggingAspect` se aplicará solo a beans cuyos nombres comiencen con `myService`.

## Conclusión

En este artículo, hemos visto cómo usar Spring AOP para implementar casos de uso comunes de AOP, como el registro, la auditoría y la supervisión del rendimiento. También hemos visto cómo usar cortes de puntos y consejos para aplicar selectivamente aspectos a beans en nuestro contexto de aplicación.

Con Spring AOP, podemos modularizar nuestras inquietudes y aplicarlas a los beans de nuestra aplicación de manera consistente y declarativa.