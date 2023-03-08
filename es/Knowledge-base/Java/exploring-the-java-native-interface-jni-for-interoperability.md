---
title: Exploración de la interfaz nativa de Java (JNI) para la interoperabilidad
description: 
published: true
date: 2023-02-06T20:56:09.911Z
tags: 
editor: markdown
dateCreated: 2023-02-06T20:56:08.251Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Exploring the Java Native Interface (JNI) for Interoperability***English** document is available*](/en/Knowledge-base/Java/exploring-the-java-native-interface-jni-for-interoperability)
{.links-list}


# Exploración de la interfaz nativa de Java (JNI) para la interoperabilidad

La interfaz nativa de Java (JNI) es una poderosa herramienta que permite que el código Java interactúe con el código nativo escrito en otros lenguajes. En este artículo, veremos más de cerca cómo funciona JNI y cómo se puede utilizar para mejorar el rendimiento de las aplicaciones Java.

## ¿Qué es la interfaz nativa de Java?

La interfaz nativa de Java es un conjunto de estándares que definen cómo el código Java puede interactuar con el código nativo escrito en otros lenguajes. JNI es independiente de la plataforma, lo que significa que se puede usar para escribir código que se ejecuta en cualquier sistema operativo.

## ¿Cómo funciona JNI?

JNI define un conjunto de reglas que rigen cómo pueden interactuar el código Java y el código nativo. Cuando una aplicación Java llama a un método nativo, la capa JNI traduce la llamada al método al idioma nativo. A continuación, se ejecuta el código nativo y el resultado se devuelve a la aplicación Java.

## Beneficios de usar JNI

Hay varios beneficios al usar JNI, que incluyen:

- Rendimiento mejorado: el código nativo suele ser más rápido que el código Java, por lo que el uso de JNI puede mejorar el rendimiento de las aplicaciones Java.
- Acceso a bibliotecas nativas: JNI permite que el código Java acceda a bibliotecas nativas que no están disponibles en la plataforma Java.
- Desarrollo simplificado: JNI se puede utilizar para escribir código que es más difícil de escribir en Java, como el código que interactúa con los componentes del sistema de bajo nivel.

## Inconvenientes de usar JNI

También hay algunos inconvenientes en el uso de JNI, que incluyen:

- Mayor complejidad: JNI agrega una capa adicional de complejidad a las aplicaciones Java.
- Portabilidad limitada: el código JNI no es portátil entre plataformas, por lo que debe reescribirse para cada plataforma.
- Riesgos de seguridad: el código JNI puede eludir el modelo de seguridad de Java, lo que puede presentar riesgos de seguridad.

## ¿Cuándo se debe usar JNI?

JNI debe usarse cuando los beneficios superan los inconvenientes. JNI se usa más comúnmente para mejorar el rendimiento de las aplicaciones Java o para acceder a bibliotecas nativas que no están disponibles en la plataforma Java.

## Ejemplo: llamar a un método nativo

Echemos un vistazo a un ejemplo de cómo se puede utilizar JNI para mejorar el rendimiento de una aplicación Java. Comenzaremos con un método Java simple que calcula la suma de dos números enteros:

```java
public static int sum(int a, int b) {
    return a + b;
}
```

Podemos mejorar el rendimiento de este método utilizando JNI para llamar a un método nativo que realiza el cálculo en código nativo. Primero, necesitamos escribir el método nativo en C:

```c
int sum(int a, int b) {
    return a + b;
}
```

A continuación, necesitamos escribir un método contenedor de Java que llame al método nativo:

```java
public static native int sum(int a, int b);
```

Finalmente, necesitamos compilar el código C y el código Java en una biblioteca compartida. En Linux, podemos hacer esto con el siguiente comando:

```
gcc -shared -fPIC -o libsum.so sum.c
```

Luego podemos cargar la biblioteca compartida en nuestra aplicación Java con el siguiente código:

```java
System.loadLibrary("sum");
```

Ahora podemos llamar al método sum() desde nuestro código Java y el cálculo se realizará en código nativo. Esto puede mejorar el rendimiento de nuestra aplicación, ya que el código nativo suele ser más rápido que el código Java.

## Ejemplo: acceder a una biblioteca nativa

JNI también se puede utilizar para acceder a bibliotecas nativas que no están disponibles en la plataforma Java. Por ejemplo, la plataforma Java no proporciona una biblioteca nativa para acceder a la API de Win32. Sin embargo, podemos usar JNI para llamar a la API Win32 desde nuestro código Java.

Primero, necesitamos escribir un método contenedor de Java para cada función de la API de Win32 a la que queremos llamar:

```java
public static native int MessageBox(int hWnd, String lpText, String lpCaption, int uType);
```

A continuación, debemos escribir un archivo C++ que incluya los archivos de encabezado para la API de Win32 y JNI:

```c++
#include <windows.h>
#include <jni.h>
```

Luego podemos escribir la implementación de nuestro método contenedor de Java:

```c++
JNIEXPORT jint JNICALL Java_MessageBox_1MessageBox(JNIEnv *env, jclass cls, jint hWnd, jstring lpText, jstring lpCaption, jint uType)
{
    return MessageBox(hWnd, (LPCTSTR)lpText, (LPCTSTR)lpCaption, uType);
}
```

Finalmente, necesitamos compilar nuestro código C++ en una biblioteca compartida. En Windows, podemos hacer esto con el siguiente comando:

```
cl /LD MessageBox.cpp
```

Luego podemos cargar la biblioteca compartida en nuestra aplicación Java con el siguiente código:

```java
System.loadLibrary("MessageBox");
```

Ahora podemos llamar a la función MessageBox() desde nuestro código Java y se llamará a la API de Win32. Esto nos permite acceder a la API Win32 desde nuestro código Java, aunque la plataforma Java no proporciona una biblioteca nativa para la API Win32.

## Ejemplo: llamar a un método Java desde código nativo

JNI también se puede usar para llamar a métodos Java desde código nativo. Esto puede ser útil cuando necesitamos llamar a un método Java desde una biblioteca nativa que no tiene una interfaz JNI.

Primero, necesitamos escribir un método contenedor de Java para el método Java que queremos llamar:

```java
public static native void print(String msg);
```

A continuación, necesitamos escribir un archivo C++ que incluya los archivos de encabezado para JNI:

```c++
#include <jni.h>
```

Luego podemos escribir la implementación de nuestro método contenedor de Java:

```c++
JNIEXPORT void JNICALL Java_print_1print(JNIEnv *env, jclass cls, jstring msg)
{
    // Get the printStream field from the java.lang.System class
    jclass systemClass = env->FindClass("java/lang/System");
    jfieldID printStreamField = env->GetStaticFieldID(systemClass, "out", "Ljava/io/PrintStream;");

    // Get the PrintStream object from the printStream field
    jobject printStream = env->GetStaticObjectField(systemClass, printStreamField);

    // Get the println() method from the PrintStream class
    jclass printStreamClass = env->GetObjectClass(printStream);
    jmethodID printlnMethod = env->GetMethodID(printStreamClass, "println", "(Ljava/lang/String;)V");

    // Call the println() method
    env->CallVoidMethod(printStream, printlnMethod, msg);
}
```

Finalmente, necesitamos compilar nuestro código C++ en una biblioteca compartida. En Windows, podemos hacer esto con el siguiente comando:

```
cl /LD print.cpp
```

Luego podemos cargar la biblioteca compartida en nuestra aplicación Java con el siguiente código:

```java
System.loadLibrary("print");
```

Ahora podemos llamar al método print() desde nuestro código C++ y se llamará al método java println(). Esto nos permite llamar a un método Java desde una biblioteca nativa que no tiene una interfaz JNI.

## Conclusión

JNI es una poderosa herramienta que permite que el código Java interopere con el código nativo escrito en otros lenguajes. JNI se puede utilizar para mejorar el rendimiento de las aplicaciones Java o para acceder a bibliotecas nativas que no están disponibles en la plataforma Java. Sin embargo, JNI también agrega una capa adicional de complejidad a las aplicaciones Java y no es portátil entre plataformas.