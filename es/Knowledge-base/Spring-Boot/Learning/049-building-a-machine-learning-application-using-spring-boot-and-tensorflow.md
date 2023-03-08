---
title: 049: Creación de una aplicación de aprendizaje automático con Spring Boot y TensorFlow
description: 
published: true
date: 2023-02-04T15:32:45.624Z
tags: 
editor: markdown
dateCreated: 2023-02-04T15:32:43.908Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [049: Building a machine learning application using Spring Boot and TensorFlow***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/049-building-a-machine-learning-application-using-spring-boot-and-tensorflow)
{.links-list}


# 049: Construyendo una aplicación de aprendizaje automático usando Spring Boot y TensorFlow

Con los avances recientes en el aprendizaje automático, cada vez más desarrolladores buscan crear aplicaciones que puedan aprovechar estas tecnologías. En esta publicación, veremos cómo crear una aplicación de aprendizaje automático con Spring Boot y TensorFlow.

Comenzaremos analizando qué es el aprendizaje automático y cómo se puede utilizar para crear aplicaciones. Luego veremos cómo configurar un proyecto Spring Boot e integrar TensorFlow. Finalmente, veremos un ejemplo simple de cómo usar TensorFlow para construir un modelo de aprendizaje automático.

## ¿Qué es el aprendizaje automático?

El aprendizaje automático es un subcampo de la inteligencia artificial que se ocupa de la construcción y el estudio de algoritmos que pueden aprender de los datos. Estos algoritmos se pueden usar para construir modelos que pueden hacer predicciones sobre nuevos datos.

Hay dos tipos principales de aprendizaje automático: supervisado y no supervisado. El aprendizaje supervisado es donde los datos se etiquetan y el algoritmo se entrena para aprender el mapeo de los datos de entrada a las etiquetas de salida. El aprendizaje no supervisado es donde los datos no están etiquetados y el algoritmo está entrenado para aprender la estructura de los datos.

## Uso del aprendizaje automático para crear aplicaciones

El aprendizaje automático se puede utilizar para crear aplicaciones que pueden aprender y mejorar automáticamente a partir de los datos. Por ejemplo, se podría usar una aplicación de aprendizaje automático para clasificar automáticamente imágenes o detectar objetos en imágenes.

Otros ejemplos de aplicaciones de aprendizaje automático incluyen:

- Generación automática de descripciones de imágenes.
- Traducir entre idiomas
- Predecir el precio de una acción.
- Detección de actividad fraudulenta

## Configuración de un proyecto Spring Boot

Comenzaremos configurando un proyecto Spring Boot. Spring Boot es un marco que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

Usaremos Spring Initializr para crear nuestro proyecto. Spring Initializr es una herramienta basada en web que se puede utilizar para generar un proyecto Spring Boot.

Seleccionaremos las siguientes opciones:

- Proyecto: Proyecto Maven
- Idioma: Java
- Versión de arranque de primavera: 2.1.0
- Metadatos del proyecto:
  - Grupo: com.ejemplo
  - Artefacto: mi aplicación
  - Nombre: Mi aplicación
  - Descripción: Una sencilla aplicación Spring Boot
  - Nombre del paquete: com.example.myapp
- Envase: Tarro
- Versión Java: 1.8
- Dependencias:
  - Internet
  - TensorFlow

Una vez que se ha generado el proyecto, podemos importarlo a nuestro IDE de elección.

## Integrando TensorFlow

TensorFlow es una plataforma de aprendizaje automático de código abierto que se puede usar para crear y entrenar modelos de aprendizaje automático.

Para agregar TensorFlow a nuestro proyecto, necesitaremos agregar la siguiente dependencia a nuestro archivo pom.xml:

```xml
<dependency>
    <groupId>org.tensorflow</groupId>
    <artifactId>tensorflow-core</artifactId>
    <version>1.10.0</version>
</dependency>
```

## Construyendo un modelo de aprendizaje automático

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a construir nuestro modelo de aprendizaje automático.

Comenzaremos creando una nueva clase llamada MyModel. Esta clase contendrá nuestro modelo de aprendizaje automático.

```java
public class MyModel {

}
```

A continuación, necesitaremos agregar las siguientes declaraciones de importación:

```java
import org.tensorflow.Tensor;
import org.tensorflow.TensorFlow;
```

Ahora, podemos comenzar a construir nuestro modelo. Comenzaremos definiendo nuestros tensores de entrada y salida. El tensor de entrada será un tensor 2D de forma [1, 2]. El tensor de salida será un tensor 1D de forma [1].

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);
}
```

A continuación, definiremos nuestro modelo. Usaremos un modelo de regresión lineal simple.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);

    private static final LinearRegressionModel model = LinearRegressionModel.create(
        input, output);
}
```

Ahora, podemos entrenar nuestro modelo. Entrenaremos nuestro modelo para 1000 iteraciones.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);

    private static final LinearRegressionModel model = LinearRegressionModel.create(
        input, output);

    public static void main(String[] args) {
        for (int i = 0; i < 1000; i++) {
            model.train();
        }
    }
}
```

Finalmente, podemos usar nuestro modelo entrenado para hacer predicciones.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);

    private static final LinearRegressionModel model = LinearRegressionModel.create(
        input, output);

    public static void main(String[] args) {
        for (int i = 0; i < 1000; i++) {
            model.train();
        }

        Tensor<Float> prediction = model.predict(input);
        System.out.println(prediction.data());
    }
}
```

## Conclusión

En esta publicación, hemos visto cómo crear una aplicación de aprendizaje automático con Spring Boot y TensorFlow. Comenzamos analizando qué es el aprendizaje automático y cómo se puede utilizar para crear aplicaciones. Luego, analizamos cómo configurar un proyecto Spring Boot e integrar TensorFlow. Finalmente, analizamos un ejemplo simple de cómo usar TensorFlow para construir un modelo de aprendizaje automático.