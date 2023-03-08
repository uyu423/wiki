---
title: Keras
description: 
published: true
date: 2023-02-16T03:55:55.432Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:55:53.560Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Keras***English** document is available*](/en/Knowledge-base/Dictionary/keras)
{.links-list}


# Descripción general
Keras es una biblioteca de redes neuronales de código abierto escrita en Python. Está diseñado para ser simple e intuitivo para que los usuarios de todos los niveles creen e implementen modelos de aprendizaje profundo. Keras es una API de alto nivel que se puede usar con backends de TensorFlow, Theano o CNTK.

# Descripción
Keras es una biblioteca para el aprendizaje profundo, un tipo de aprendizaje automático que utiliza redes neuronales para aprender de los datos. Fue desarrollado por François Chollet, un ingeniero de Google, y lanzado en 2015. Keras está diseñado para ser intuitivo y fácil de usar, y proporciona una API de alto nivel para crear y entrenar redes neuronales.

Keras se basa en TensorFlow, Theano o CNTK, que son bibliotecas de nivel inferior para construir y entrenar redes neuronales. Proporciona una interfaz más sencilla e intuitiva para que los usuarios creen y entrenen modelos. Keras también admite redes neuronales convolucionales y recurrentes, que se utilizan para el procesamiento de imágenes y texto, respectivamente.

Keras es una opción popular para el aprendizaje profundo debido a su facilidad de uso y flexibilidad. También se utiliza en muchas aplicaciones, incluida la visión artificial, el procesamiento del lenguaje natural y el reconocimiento automático de voz.

# Características
Keras proporciona una serie de funciones para facilitar el trabajo con modelos de aprendizaje profundo. Éstas incluyen:

- **API de alto nivel:** Keras proporciona una API de alto nivel para crear y entrenar redes neuronales, lo que facilita la creación de modelos a usuarios de todos los niveles.

- **Compatibilidad:** Keras es compatible con TensorFlow, Theano y CNTK, lo que permite a los usuarios elegir el backend que mejor se adapte a sus necesidades.

- **Diseño modular:** Keras está diseñado para ser modular, lo que permite a los usuarios crear y combinar fácilmente diferentes capas y modelos.

- **Compatibilidad con redes convolucionales y recurrentes:** Keras admite redes neuronales convolucionales y recurrentes, que se utilizan para el procesamiento de imágenes y texto, respectivamente.

- **Extensibilidad:** Keras está diseñado para ser extensible, lo que permite a los usuarios crear capas y modelos personalizados.

# Ejemplo
El siguiente ejemplo muestra cómo crear una red neuronal convolucional simple usando Keras.

```python
from keras.layers import Conv2D, MaxPooling2D
from keras.models import Sequential

model = Sequential()
model.add(Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))

model.summary()
```

# Pros y contras
Keras es una opción popular para el aprendizaje profundo debido a su facilidad de uso y flexibilidad. Está diseñado para ser intuitivo y fácil de usar, y proporciona una API de alto nivel para crear y entrenar redes neuronales.

Sin embargo, Keras no es adecuado para todas las aplicaciones. No proporciona tanto control sobre el modelo como las bibliotecas de nivel inferior, como TensorFlow o Theano. Tampoco es compatible con la computación distribuida, lo que puede ser importante para proyectos a gran escala.

# Tecnología relacionada
Keras se basa en TensorFlow, Theano y CNTK, que son bibliotecas de nivel inferior para construir y entrenar redes neuronales. También está relacionado con otros marcos de aprendizaje automático como Scikit-learn y PyTorch.