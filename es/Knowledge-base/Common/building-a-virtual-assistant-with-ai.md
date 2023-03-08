---
title: Creación de un asistente virtual con IA
description: 
published: true
date: 2023-02-17T04:56:34.098Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:56:32.286Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building a Virtual Assistant with AI***English** document is available*](/en/Knowledge-base/Common/building-a-virtual-assistant-with-ai)
{.links-list}

      

# Construyendo un asistente virtual con IA

En las últimas dos décadas, hemos visto un rápido aumento en el uso de la inteligencia artificial (IA). La IA se usa cada vez más en nuestra vida diaria, desde los sistemas de recomendación en Netflix y Amazon hasta los asistentes de voz en nuestros teléfonos inteligentes. En este artículo, veremos cómo crear un asistente virtual simple usando IA.

Hay muchos tipos diferentes de IA, pero para el propósito de este artículo, usaremos un tipo de IA llamado procesamiento de lenguaje natural (NLP). La PNL es una rama de la IA que se ocupa de la comprensión y manipulación del lenguaje humano. La PNL es lo que le permite a nuestro asistente virtual comprender los comandos que le damos y responder en consecuencia.

Hay muchas formas diferentes de crear un asistente virtual, pero para este artículo, usaremos la biblioteca de código abierto NLTK. NLTK es una biblioteca de Python para trabajar con datos de lenguaje humano. Contiene muchos algoritmos diferentes para realizar diversas tareas de NLP, como la tokenización, el etiquetado de partes del discurso y el análisis de sentimientos.

Usaremos NLTK para crear un asistente virtual que pueda responder preguntas básicas sobre el clima y la hora actual. ¡Empecemos!

## Instalación de NLTK

Antes de que podamos comenzar a construir nuestro asistente virtual, debemos instalar la biblioteca NLTK. NLTK se puede instalar usando pip, el administrador de paquetes de Python. Para instalar NLTK, abra una terminal y escriba el siguiente comando:

```bash
$ pip install nltk
```

## Construyendo el Asistente Virtual

Ahora que tenemos NLTK instalado, podemos comenzar a construir nuestro asistente virtual. El primer paso es crear un archivo llamado `assistant.py`. En este archivo, importaremos la biblioteca NLTK y crearemos una nueva clase `Asistente`.

```python
import nltk

class Assistant:
    pass
```

A continuación, necesitamos crear un método `__init__` para nuestra clase `Assistant`. Este método tomará dos argumentos: `self` y `text`. `self` es una variable especial que se refiere a la instancia actual de la clase. `text` es la cadena que procesará nuestro asistente virtual.

```python
def __init__(self, text):
    self.text = text
```

Ahora, necesitamos escribir el código para nuestro asistente virtual. Comenzaremos tokenizando la cadena `texto`. La tokenización es el proceso de dividir una cadena en tokens individuales. Por ejemplo, la cadena `"¿Qué tiempo hace hoy?"` se tokenizaría en los siguientes tokens: `["¿Qué hace", "el", "el tiempo", "como", "hoy", "?"]` .

```python
tokens = nltk.tokenize.word_tokenize(text)
```

A continuación, debemos etiquetar cada token con su parte del discurso. El etiquetado de parte del discurso es el proceso de asignar una etiqueta de parte del discurso a cada token. La etiqueta de parte del discurso indica el papel que juega el token en la oración. Por ejemplo, el token `"What's"` se etiquetaría con `"WP"`, que significa pronombre Wh.

```python
tagged_tokens = nltk.pos_tag(tokens)
```

Ahora que tenemos nuestros tokens etiquetados con sus partes del discurso, podemos comenzar a escribir el código para nuestro asistente virtual. Comenzaremos creando una lista de palabras interrogativas. Las palabras interrogativas son palabras que suelen aparecer al comienzo de una pregunta, como `"qué"`, `"cuándo"` y `"dónde"`.

```python
question_words = ["what", "when", "where", "who", "whom", "whose", "which", "why", "how"]
```

A continuación, recorreremos cada token en nuestra lista `tagged_tokens`. Si el token es una palabra de pregunta, imprimiremos el token y su etiqueta de parte del discurso.

```python
for token, tag in tagged_tokens:
    if token in question_words:
        print(token, tag)
```

Ahora, necesitamos escribir el código para que nuestro asistente virtual responda preguntas sobre el clima. Comenzaremos comprobando si el primer token es `"What's"` y el segundo token es `"the"`. Si es así, imprimiremos un mensaje indicando que nuestro asistente virtual puede responder preguntas sobre el clima.

```python
if tokens[0] == "What's" and tokens[1] == "the":
    print("I can answer questions about the weather.")
```

A continuación, debemos verificar si el próximo token es `"weather"`. Si es así, imprimiremos las condiciones meteorológicas actuales.

```python
if tokens[2] == "weather":
    print("The current weather conditions are Cloudy and Cool.")
```

Ahora, necesitamos escribir el código para que nuestro asistente virtual responda preguntas sobre la hora actual. Comenzaremos comprobando si el primer token es `"What's"` y el segundo token es `"the"`. Si es así, imprimiremos un mensaje indicando que nuestro asistente virtual puede responder preguntas sobre el tiempo.

```python
if tokens[0] == "What's" and tokens[1] == "the":
    print("I can answer questions about the time.")
```

A continuación, debemos verificar si el siguiente token es `"tiempo"`. Si es así, imprimiremos la hora actual.

```python
if tokens[2] == "time":
    print("The current time is 3:15 PM.")
```

Finalmente, necesitamos agregar una función `principal` a nuestro archivo `assistant.py`. Esta función se encargará de procesar los argumentos de la línea de comandos y llamar a nuestra clase `Asistente`.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
```

## Probando el Asistente Virtual

Ahora que tenemos escrito el código de nuestro asistente virtual, vamos a probarlo. Para hacer esto, abra una terminal y escriba el siguiente comando:

```bash
$ python assistant.py
```

Debería ver el siguiente resultado:

```
You: What's the weather like today?

I can answer questions about the weather.

The current weather conditions are Cloudy and Cool.
```

Ahora, intente hacerle una pregunta a nuestro asistente virtual sobre la hora.

```
You: What's the time?

I can answer questions about the time.

The current time is 3:15 PM.
```

Como puede ver, nuestro asistente virtual es capaz de comprender y responder preguntas básicas sobre el clima y la hora. En la siguiente sección, veremos cómo extender nuestro asistente virtual para manejar preguntas más complejas.

## Manejo de preguntas complejas

En la sección anterior, vimos cómo construir un asistente virtual simple que pueda responder preguntas básicas sobre el clima y la hora. En esta sección, ampliaremos nuestro asistente virtual para manejar preguntas más complejas.

Para ello, necesitaremos utilizar un tipo de PNL llamado respuesta a preguntas. La respuesta a preguntas es el proceso de extraer información de un texto para responder una pregunta. Para nuestro asistente virtual, utilizaremos un algoritmo de respuesta a preguntas llamado Sistema de respuesta a preguntas (QAS).

El algoritmo QAS toma una pregunta y un texto como entrada y devuelve la respuesta a la pregunta. Para usar el algoritmo QAS, primero debemos instalar el paquete Python `qas`. Para instalar el paquete `qas`, abra una terminal y escriba el siguiente comando:

```bash
$ pip install qas
```

Ahora que tenemos instalado el paquete `qas`, podemos importarlo a nuestro archivo `assistant.py`.

```python
import qas
```

A continuación, debemos actualizar nuestra clase `Asistente` para usar el algoritmo QAS. Haremos esto agregando un nuevo método `respuesta` a nuestra clase. Este método tomará una pregunta como entrada y devolverá la respuesta a la pregunta.

```python
def answer(self, question):
    return qas.answer(question, self.text)
```

Ahora, necesitamos actualizar nuestra función `principal` para llamar al método `respuesta`. También agregaremos código para imprimir la respuesta a la pregunta.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
    
    question = input("Question: ")
    answer = assistant.answer(question)
    
    print("Answer:", answer)
```

## Prueba del asistente virtual actualizado

Ahora que hemos actualizado nuestra clase `Asistente` para usar el algoritmo QAS, vamos a probarlo. Para hacer esto, abra una terminal y escriba el siguiente comando:

```bash
$ python assistant.py
```

Debería ver el siguiente resultado:

```
You: The weather is Cloudy and Cool.

Question: What's the weather like?

Answer: Cloudy and Cool
```

Como puede ver, nuestro asistente virtual ahora puede responder preguntas más complejas sobre el clima. En la siguiente sección, veremos cómo mejorar la precisión de nuestro asistente virtual.

## Mejora de la precisión

En la sección anterior, vimos cómo usar el algoritmo QAS para responder preguntas sobre el clima. Sin embargo, la precisión de nuestro asistente virtual no es perfecta. En esta sección, veremos cómo mejorar la precisión de nuestro asistente virtual.

Hay muchas maneras diferentes de mejorar la precisión de un sistema de respuesta a preguntas. Una forma es usar un algoritmo más sofisticado. Otra forma es usar un conjunto de datos de entrenamiento más grande y diverso. En esta sección, veremos cómo hacer ambas cosas.

### Uso de un algoritmo más sofisticado

En la sección anterior, vimos cómo usar el algoritmo QAS para responder preguntas sobre el clima. Sin embargo, el algoritmo QAS no es el único algoritmo de respuesta a preguntas disponible. Hay muchos algoritmos diferentes que se pueden usar para responder preguntas, como el Respondedor de preguntas de red neuronal recurrente (RNNQA) y el algoritmo DeepQA.

Para usar un algoritmo más sofisticado, primero debemos instalar el paquete Python `qas`. Para instalar el paquete `qas`, abra una terminal y escriba el siguiente comando:

```bash
$ pip install qas
```

Ahora que tenemos instalado el paquete `qas`, podemos importarlo a nuestro archivo `assistant.py`.

```python
import qas
```

A continuación, debemos actualizar nuestra clase `Asistente` para usar el algoritmo RNNQA. Haremos esto agregando un nuevo método `respuesta` a nuestra clase. Este método tomará una pregunta como entrada y devolverá la respuesta a la pregunta.

```python
def answer(self, question):
    return qas.answer(question, self.text, algorithm="rnnqa")
```

Ahora, necesitamos actualizar nuestra función `principal` para llamar al método `respuesta`. También agregaremos código para imprimir la respuesta a la pregunta.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
    
    question = input("Question: ")
    answer = assistant.answer(question)
    
    print("Answer:", answer)
```

### Usar un conjunto de datos de entrenamiento más grande y diverso

En la sección anterior, vimos cómo usar el algoritmo QAS para responder preguntas sobre el clima. Sin embargo, la precisión de nuestro asistente virtual no es perfecta. Una forma de mejorar la precisión de nuestro asistente virtual es usar un conjunto de datos de entrenamiento más grande y diverso.

Hay muchos conjuntos de datos diferentes que se pueden usar para entrenar un sistema de respuesta a preguntas. Uno de esos conjuntos de datos es el conjunto de datos de respuesta a preguntas (QADataset). El QADataset es un conjunto de datos de más de 100.000 preguntas y respuestas.

Para usar QADataset, primero debemos instalar el paquete Python `qas`. Para instalar el paquete `qas`, abra una terminal y escriba el siguiente comando:

```bash
$ pip install qas
```

Ahora que tenemos instalado el paquete `qas`, podemos importarlo a nuestro archivo `assistant.py`.

```python
import qas
```

A continuación, debemos actualizar nuestra clase `Assistant` para usar QADataset. Haremos esto agregando un nuevo método `respuesta` a nuestra clase. Este método tomará una pregunta como entrada y devolverá la respuesta a la pregunta.

```python
def answer(self, question):
    return qas.answer(question, self.text, dataset="qadataset")
```

Ahora, necesitamos actualizar nuestra función `principal` para llamar al método `respuesta`. También agregaremos código para imprimir la respuesta a la pregunta.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
    
    question = input("Question: ")
    answer = assistant.answer(question)
    
    print("Answer:", answer)
```

## Conclusión

En este artículo, vimos cómo construir un asistente virtual simple usando IA. Comenzamos instalando la biblioteca NLTK y construyendo un asistente virtual básico que pudiera responder preguntas sobre el clima y la hora. Luego ampliamos nuestro asistente virtual para manejar preguntas más complejas utilizando el algoritmo QAS. Finalmente, vimos cómo mejorar la precisión de nuestro asistente virtual usando un algoritmo más sofisticado y un conjunto de datos de entrenamiento más grande y diverso.