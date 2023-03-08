---
title: Uso de clases trazables e instrumentadas de Java para monitoreo
description: 
published: true
date: 2023-02-05T12:17:30.168Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:17:28.500Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using Java's Traceable and Instrumented Classes for Monitoring***English** document is available*](/en/Knowledge-base/Java/using-java-s-traceable-and-instrumented-classes-for-monitoring)
{.links-list}


# Uso de las clases trazables e instrumentadas de Java para el monitoreo

El código de instrumentación es una técnica poderosa para monitorear el rendimiento de las aplicaciones Java. Mediante el uso de las clases rastreables e instrumentadas de Java, los desarrolladores pueden recopilar información detallada sobre cómo se ejecuta su código e identificar posibles cuellos de botella.

La instrumentación se puede usar para monitorear muchos aspectos del rendimiento de una aplicación, incluido el uso de la memoria, la actividad de recolección de elementos no utilizados y la ejecución de subprocesos. En este artículo, nos centraremos en el uso de instrumentación para monitorear los tiempos de ejecución de métodos.

## ¿Por qué usar instrumentación?

La instrumentación permite a los desarrolladores recopilar datos de rendimiento sin tener que modificar su código. Esto es especialmente útil para monitorear sistemas de producción, donde los cambios de código pueden ser difíciles de implementar.

La instrumentación también se puede usar para monitorear el código que no está bajo el control del desarrollador, como las bibliotecas de terceros. En este caso, la instrumentación se puede utilizar para recopilar datos sobre cómo se utiliza la biblioteca e identificar posibles problemas de rendimiento.

## Uso de las clases trazables e instrumentadas de Java

Las clases rastreables e instrumentadas de Java proporcionan una forma sencilla de instrumentar el código y recopilar datos de rendimiento. Estas clases son parte del paquete java.lang.instrument y están disponibles en Java 5 y versiones posteriores.

Para usar las clases Traceable e Instrumented, los desarrolladores deben crear una subclase de java.lang.instrument.Instrumentation y anular el método premain(). Este método se llama antes de que se ejecute el método main() de la aplicación.

En el método premain(), el desarrollador necesita crear una instancia de su subclase rastreable o instrumentada y registrarla con la máquina virtual de Java (JVM). La JVM luego llamará a los métodos en la subclase Traceable o Instrumented cuando ocurran ciertos eventos, como la invocación de un método.

Aquí hay un ejemplo simple de una subclase rastreable que rastrea los tiempos de invocación del método:

```java
public class MyTraceable extends Traceable {

private Map<String, Long> methodTimes = new HashMap<String, Long>();

@Override
public void traceMethodInvocation(MethodInfo methodInfo) {

String methodName = methodInfo.getMethodName();

if (methodTimes.containsKey(methodName)) {

long totalTime = methodTimes.get(methodName);

totalTime += methodInfo.getElapsedTime();

methodTimes.put(methodName, totalTime);

} else {

methodTimes.put(methodName, methodInfo.getElapsedTime());

}

}

public Map<String, Long> getMethodTimes() {

return methodTimes;

}

}
```

En el ejemplo anterior, se llama al método traceMethodInvocation() cada vez que se invoca un método. El parámetro methodInfo contiene información sobre el método, incluido el nombre del método y la cantidad de tiempo que tardó en ejecutarse.

El método traceMethodInvocation() almacena los tiempos de invocación del método en un mapa. El método getMethodTimes() se puede utilizar para recuperar el mapa.

Para registrar la clase MyTraceable con la JVM, se puede usar el método premain():

```java
public static void premain(String args, Instrumentation instrumentation) {

instrumentation.addTransformer(new MyTraceable());

}
```

En el método premain(), la clase MyTraceable se registra con el objeto de instrumentación. El objeto de instrumentación se usa para agregar transformadores de clase a la JVM. Un transformador de clase es una pieza de código que modifica el código de bytes de una clase antes de que la JVM la cargue.

La clase MyTraceable se registra como un transformador de clase para que se llame a su método traceMethodInvocation() cada vez que se invoque un método.

Una vez registrada la clase MyTraceable, la aplicación se puede ejecutar como de costumbre. Se llamará al método traceMethodInvocation() cada vez que se invoque un método y se realizará un seguimiento de los tiempos de invocación del método en el objeto MyTraceable.

## Analizando los datos

Los datos recopilados por la clase MyTraceable se pueden utilizar para identificar posibles cuellos de botella en la aplicación. Para hacer esto, los datos se pueden ordenar por la cantidad de tiempo empleado en cada método.

Los métodos que tardan más tiempo en ejecutarse son cuellos de botella potenciales. Estos métodos se pueden analizar más a fondo para ver si se pueden optimizar.

## Conclusión

La instrumentación es una técnica poderosa para monitorear el desempeño de las aplicaciones Java. Mediante el uso de las clases rastreables e instrumentadas de Java, los desarrolladores pueden recopilar información detallada sobre cómo se ejecuta su código e identificar posibles cuellos de botella.