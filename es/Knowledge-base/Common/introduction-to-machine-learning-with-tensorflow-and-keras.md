---
title: Introducción al aprendizaje automático con TensorFlow y Keras
description: 
published: true
date: 2023-02-09T22:55:38.958Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:55:32.562Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Introduction to Machine Learning with TensorFlow and Keras***English** document is available*](/en/Knowledge-base/Common/introduction-to-machine-learning-with-tensorflow-and-keras)
{.links-list}


# Introducción al aprendizaje automático con TensorFlow y Keras

Los desarrolladores que buscan agregar aprendizaje automático a sus aplicaciones tienen muchas opciones para elegir cuando se trata de marcos y bibliotecas. TensorFlow y Keras son dos de las opciones más populares para el aprendizaje profundo y, en este artículo, veremos cómo comenzar con ambos.

## Flujo de tensor

TensorFlow es una popular plataforma de código abierto para el aprendizaje automático desarrollada por Google. Ofrece una amplia gama de herramientas, bibliotecas y recursos comunitarios que permiten a los desarrolladores crear modelos sofisticados de aprendizaje automático con facilidad.

TensorFlow también tiene un fuerte enfoque en las implementaciones de producción y ofrece una serie de características que facilitan la implementación de modelos de aprendizaje automático en servicios y dispositivos.

## Keras

Keras es una API de aprendizaje profundo de alto nivel desarrollada con un enfoque en la facilidad de uso y el desarrollo rápido. Está construido sobre TensorFlow y se puede usar para crear modelos sofisticados de aprendizaje automático con un código mínimo.

Keras también es una opción popular para la creación de prototipos y la investigación, ya que ofrece una manera simple y eficiente de construir y experimentar con modelos de aprendizaje profundo.

## Empezando

En esta sección, veremos cómo comenzar con TensorFlow y Keras. Comenzaremos instalando las dependencias requeridas y luego veremos algunos ejemplos de código básicos.

### Instalación

Antes de que podamos comenzar a usar TensorFlow y Keras, debemos instalar las dependencias requeridas. TensorFlow se puede instalar usando pip:

```
pip install tensorflow
```

Keras también se puede instalar usando pip:

```
pip install keras
```

### Hola, TensorFlow

Ahora que tenemos instalados TensorFlow y Keras, echemos un vistazo a un ejemplo simple. Comenzaremos importando la biblioteca TensorFlow:

```python
import tensorflow as tf
```

A continuación, crearemos una constante de TensorFlow:

```python
tf.constant('Hello, TensorFlow!')
```

Este código imprimirá la cadena "¡Hola, TensorFlow!" a la consola

### Hola Keras

Ahora echemos un vistazo a un ejemplo simple de Keras. Comenzaremos importando la biblioteca de Keras:

```python
import keras
```

A continuación, crearemos un modelo secuencial de Keras:

```python
model = keras.Sequential()
```

Este código creará un modelo secuencial de Keras simple. Luego podemos agregar capas al modelo usando el método .add():

```python
model.add(keras.layers.Dense(units=32, input_shape=(784,)))
model.add(keras.layers.Activation('relu'))
model.add(keras.layers.Dense(units=10))
model.add(keras.layers.Activation('softmax'))
```

Este código agregará una capa densa con 32 neuronas, una capa de activación, una capa densa con 10 neuronas y una capa de activación.

Luego podemos compilar el modelo usando el método .compile():

```python
model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
```

Este código compilará el modelo utilizando la función de pérdida de entropía cruzada categórica, el optimizador de descenso de gradiente estocástico y la métrica de precisión.

Luego podemos ajustar el modelo a los datos usando el método .fit():

```python
model.fit(x_train, y_train,
          batch_size=128, epochs=5,
          verbose=1,
          validation_data=(x_test, y_test))
```

Este código ajustará el modelo a los datos de entrenamiento durante 5 épocas. El modelo se entrenará usando mini lotes de tamaño 128. El método .fit() también toma un argumento de validación_datos, que se usa para evaluar el modelo durante el entrenamiento.

Luego podemos evaluar el modelo usando el método .evaluate():

```python
score = model.evaluate(x_test, y_test, verbose=0)
```

Este código evaluará el modelo en los datos de prueba y devolverá la pérdida y la precisión.

## Conclusión

En este artículo, echamos un vistazo a cómo comenzar con TensorFlow y Keras. Hemos instalado las dependencias requeridas y miramos algunos ejemplos de código básicos.

Si está interesado en obtener más información sobre TensorFlow y Keras, le recomiendo que consulte los siguientes recursos:

- El sitio web de TensorFlow: https://www.tensorflow.org/
- El sitio web de Keras: https://keras.io/
- La documentación de TensorFlow: https://www.tensorflow.org/docs/
- La documentación de Keras: https://keras.io/docs/