---
title: 095: Creación de un sistema de aprendizaje automático con Spring Boot y TensorFlow
description: 
published: true
date: 2023-02-06T00:32:33.375Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:32:31.740Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [095: Building a Machine Learning System with Spring Boot and TensorFlow***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/095-building-a-machine-learning-system-with-spring-boot-and-tensorflow)
{.links-list}


# 095: Construcción de un Sistema de Aprendizaje Automático con Spring Boot y TensorFlow

En esta publicación, aprenderemos cómo crear un sistema de aprendizaje automático con Spring Boot y TensorFlow. Pasaremos por el proceso de configurar un entorno de desarrollo, entrenar un modelo e implementar el modelo entrenado en una aplicación web.

## Configuración del entorno de desarrollo

Lo primero que tenemos que hacer es configurar nuestro entorno de desarrollo. Necesitaremos instalar el siguiente software:

-Java8
- Experto
- TensorFlow

Podemos instalar Java 8 y Maven usando nuestro administrador de paquetes favorito. Para TensorFlow, necesitaremos descargar los archivos binarios del [sitio web de TensorFlow] (https://www.tensorflow.org/). Una vez que tengamos todo instalado, podemos crear un nuevo proyecto Maven y agregar las siguientes dependencias a nuestro archivo `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.tensorflow</groupId>
        <artifactId>tensorflow-core</artifactId>
        <version>1.15.0</version>
    </dependency>
</dependencies>
```

## Entrenando al modelo

Ahora que tenemos configurado nuestro entorno de desarrollo, podemos comenzar a entrenar nuestro modelo de aprendizaje automático. Usaremos el conjunto de datos [MNIST](https://en.wikipedia.org/wiki/MNIST_database) para este ejemplo. El conjunto de datos MNIST es una colección de dígitos escritos a mano que se usa comúnmente para entrenar modelos de reconocimiento de imágenes.

Comenzaremos creando una nueva clase Java llamada `MnistClassifier.java`. En esta clase, usaremos TensorFlow para entrenar una red neuronal simple para clasificar dígitos MNIST. Usaremos la API [Keras](https://keras.io/) para simplificar el desarrollo de nuestra red neuronal.

Primero, necesitaremos importar los siguientes paquetes:

```java
import org.tensorflow.keras.datasets.mnist.MnistDataset;
import org.tensorflow.keras.models.Sequential;
import org.tensorflow.keras.layers.Dense;
import org.tensorflow.keras.optimizers.SGD;
```

A continuación, cargaremos el conjunto de datos MNIST:

```java
MnistDataset dataset = MnistDataset.create();
```

Ahora, podemos crear nuestra red neuronal:

```java
Sequential model = new Sequential();
model.add(new Dense(128, activation="relu", inputShape=(784,)));
model.add(new Dense(10, activation="softmax"));
```

Ahora podemos compilar y entrenar nuestro modelo:

```java
model.compile(
    optimizer=new SGD(0.001),
    loss="categorical_crossentropy",
    metrics=["accuracy"]
);
model.fit(
    dataset.getTrainImages(), dataset.getTrainLabels(),
    epochs=10, batchSize=128
);
```

## Desplegando el modelo entrenado

Ahora que tenemos un modelo entrenado, podemos implementarlo en una aplicación web. Usaremos Spring Boot para simplificar el desarrollo de nuestra aplicación web.

Primero, necesitaremos crear una nueva clase Java llamada `MnistController.java`. En esta clase, crearemos un controlador REST que expone un punto final `/classify`. Este punto final tomará una imagen de un dígito escrito a mano y devolverá el dígito predicho.

Comenzaremos importando los siguientes paquetes:

```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
```

A continuación, crearemos nuestra clase `MnistController` y la anotaremos con `@RestController`:

```java
@RestController
public class MnistController {

}
```

Ahora, podemos crear nuestro punto final `/classify`:

```java
@PostMapping("/classify")
public String classify(@RequestParam("image") String image) {
    // TODO: Classify the image and return the predicted digit
}
```

En el método `clasificar`, necesitaremos clasificar la imagen y devolver el dígito predicho. Podemos hacer esto usando nuestra clase `MnistClassifier` entrenada:

```java
MnistClassifier classifier = new MnistClassifier();
String predictedDigit = classifier.classify(image);
return predictedDigit;
```

## Conclusión

En esta publicación, aprendimos cómo construir un sistema de aprendizaje automático usando Spring Boot y TensorFlow. Pasamos por el proceso de configurar un entorno de desarrollo, entrenar un modelo e implementar el modelo entrenado en una aplicación web.