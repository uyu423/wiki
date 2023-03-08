---
title: 095: Building a Machine Learning System with Spring Boot and TensorFlow
description: 
published: true
date: 2023-02-06T00:32:37.297Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:32:31.743Z
---

- [095: Creación de un sistema de aprendizaje automático con Spring Boot y TensorFlow***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/095-building-a-machine-learning-system-with-spring-boot-and-tensorflow)
{.links-list}
- [095：使用 Spring Boot 和 TensorFlow 构建机器学习系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/095-building-a-machine-learning-system-with-spring-boot-and-tensorflow)
{.links-list}
- [095: Spring Boot 및 TensorFlow를 사용하여 기계 학습 시스템 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/095-building-a-machine-learning-system-with-spring-boot-and-tensorflow)
{.links-list}


# 095: Building a Machine Learning System with Spring Boot and TensorFlow

In this post, we'll learn how to build a machine learning system using Spring Boot and TensorFlow. We'll go through the process of setting up a development environment, training a model, and deploying the trained model to a web application.

## Setting up the development environment

The first thing we need to do is set up our development environment. We'll need to install the following software:

- Java 8
- Maven
- TensorFlow

We can install Java 8 and Maven using our favorite package manager. For TensorFlow, we'll need to download the binaries from the [TensorFlow website](https://www.tensorflow.org/). Once we have everything installed, we can create a new Maven project and add the following dependencies to our `pom.xml` file:

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

## Training the model

Now that we have our development environment set up, we can start training our machine learning model. We'll use the [MNIST](https://en.wikipedia.org/wiki/MNIST_database) dataset for this example. The MNIST dataset is a collection of handwritten digits that is commonly used for training image recognition models.

We'll start by creating a new Java class called `MnistClassifier.java`. In this class, we'll use TensorFlow to train a simple neural network to classify MNIST digits. We'll use the [Keras](https://keras.io/) API to simplify the development of our neural network.

First, we'll need to import the following packages:

```java
import org.tensorflow.keras.datasets.mnist.MnistDataset;
import org.tensorflow.keras.models.Sequential;
import org.tensorflow.keras.layers.Dense;
import org.tensorflow.keras.optimizers.SGD;
```

Next, we'll load the MNIST dataset:

```java
MnistDataset dataset = MnistDataset.create();
```

Now, we can create our neural network:

```java
Sequential model = new Sequential();
model.add(new Dense(128, activation="relu", inputShape=(784,)));
model.add(new Dense(10, activation="softmax"));
```

We can now compile and train our model:

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

## Deploying the trained model

Now that we have a trained model, we can deploy it to a web application. We'll use Spring Boot to simplify the development of our web application.

First, we'll need to create a new Java class called `MnistController.java`. In this class, we'll create a REST controller that exposes a `/classify` endpoint. This endpoint will take an image of a handwritten digit and return the predicted digit.

We'll start by importing the following packages:

```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
```

Next, we'll create our `MnistController` class and annotate it with `@RestController`:

```java
@RestController
public class MnistController {

}
```

Now, we can create our `/classify` endpoint:

```java
@PostMapping("/classify")
public String classify(@RequestParam("image") String image) {
    // TODO: Classify the image and return the predicted digit
}
```

In the `classify` method, we'll need to classify the image and return the predicted digit. We can do this by using our trained `MnistClassifier` class:

```java
MnistClassifier classifier = new MnistClassifier();
String predictedDigit = classifier.classify(image);
return predictedDigit;
```

## Conclusion

In this post, we learned how to build a machine learning system using Spring Boot and TensorFlow. We went through the process of setting up a development environment, training a model, and deploying the trained model to a web application.