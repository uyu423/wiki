---
title: 095：使用 Spring Boot 和 TensorFlow 构建机器学习系统
description: 
published: true
date: 2023-02-06T00:32:33.310Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:32:31.737Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [095: Building a Machine Learning System with Spring Boot and TensorFlow***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/095-building-a-machine-learning-system-with-spring-boot-and-tensorflow)
{.links-list}


# 095：使用 Spring Boot 和 TensorFlow 构建机器学习系统

在本文中，我们将学习如何使用 Spring Boot 和 TensorFlow 构建机器学习系统。我们将完成设置开发环境、训练模型以及将训练后的模型部署到 Web 应用程序的过程。

## 搭建开发环境

我们需要做的第一件事是设置我们的开发环境。我们需要安装以下软件：

- Java 8
- 专家
- 张量流

我们可以使用我们最喜欢的包管理器安装 Java 8 和 Maven。对于 TensorFlow，我们需要从 [TensorFlow 网站](https://www.tensorflow.org/) 下载二进制文件。一旦我们安装了所有东西，我们就可以创建一个新的 Maven 项目并将以下依赖项添加到我们的 pom.xml 文件中：

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

## 训练模型

现在我们已经设置了开发环境，可以开始训练我们的机器学习模型了。我们将在此示例中使用 [MNIST](https://en.wikipedia.org/wiki/MNIST_database) 数据集。 MNIST 数据集是手写数字的集合，通常用于训练图像识别模型。

我们将从创建一个名为“MnistClassifier.java”的新 Java 类开始。在本课程中，我们将使用 TensorFlow 训练一个简单的神经网络来对 MNIST 数字进行分类。我们将使用 [Keras](https://keras.io/) API 来简化神经网络的开发。

首先，我们需要导入以下包：

```java
import org.tensorflow.keras.datasets.mnist.MnistDataset;
import org.tensorflow.keras.models.Sequential;
import org.tensorflow.keras.layers.Dense;
import org.tensorflow.keras.optimizers.SGD;
```

接下来，我们将加载 MNIST 数据集：

```java
MnistDataset dataset = MnistDataset.create();
```

现在，我们可以创建我们的神经网络：

```java
Sequential model = new Sequential();
model.add(new Dense(128, activation="relu", inputShape=(784,)));
model.add(new Dense(10, activation="softmax"));
```

我们现在可以编译和训练我们的模型：

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

## 部署训练好的模型

现在我们有了经过训练的模型，我们可以将它部署到 Web 应用程序中。我们将使用 Spring Boot 来简化 Web 应用程序的开发。

首先，我们需要创建一个名为“MnistController.java”的新 Java 类。在这个类中，我们将创建一个 REST 控制器，它公开一个 `/classify` 端点。此端点将拍摄手写数字的图像并返回预测数字。

我们将从导入以下包开始：

```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
```

接下来，我们将创建我们的“MnistController”类并使用“@RestController”对其进行注释：

```java
@RestController
public class MnistController {

}
```

现在，我们可以创建我们的 `/classify` 端点：

```java
@PostMapping("/classify")
public String classify(@RequestParam("image") String image) {
    // TODO: Classify the image and return the predicted digit
}
```

在 classify 方法中，我们需要对图像进行分类并返回预测数字。我们可以通过使用我们训练有素的“MnistClassifier”类来做到这一点：

```java
MnistClassifier classifier = new MnistClassifier();
String predictedDigit = classifier.classify(image);
return predictedDigit;
```

## 结论

在本文中，我们学习了如何使用 Spring Boot 和 TensorFlow 构建机器学习系统。我们经历了搭建开发环境、训练模型以及将训练好的模型部署到 Web 应用程序的过程。