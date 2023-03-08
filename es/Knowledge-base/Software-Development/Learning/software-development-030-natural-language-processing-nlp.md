---
title: Desarrollo de software 030: Procesamiento del lenguaje natural (PNL)
description: 
published: true
date: 2023-02-09T15:56:24.260Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:56:22.591Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 030: Natural Language Processing (NLP)***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-030-natural-language-processing-nlp)
{.links-list}


# Desarrollo de software 030: Procesamiento del lenguaje natural (PNL)

En esta publicación, analizaremos de manera integral y práctica el procesamiento del lenguaje natural (PNL). Cubriremos qué es NLP, algunas de las tareas para las que se usa y cómo comenzar a codificar en Python.

## ¿Qué es la PNL?

El procesamiento del lenguaje natural (NLP) es un campo de la informática y la inteligencia artificial que se ocupa de las interacciones entre las computadoras y los lenguajes humanos (naturales), en particular, cómo programar las computadoras para procesar y analizar grandes cantidades de datos del lenguaje natural.

NLP se utiliza para crear aplicaciones como chatbots, reconocimiento automático de voz y traducción automática.

## Tareas de PNL

Hay muchas tareas diferentes que se pueden realizar con PNL. Algunas de las tareas más comunes son:

- **Clasificación de texto:** Asignar una categoría o etiqueta a un fragmento de texto, p. detección de spam, análisis de sentimientos.

- **Extracción de información:** Extracción de datos estructurados de texto no estructurado, p. extraer fechas, nombres y ubicaciones de un documento.

- **Generación de lenguaje natural:** Generación de texto a partir de datos, p. generar un resumen de un documento.

- **Reconocimiento de voz:** Conversión de voz a texto, p. aplicaciones de voz a texto.

- **Traducción automática:** traducir texto de un idioma a otro, p. Google Translate.

## Primeros pasos con la PNL

En esta sección, cubriremos los conceptos básicos de la codificación en Python para NLP. Usaremos Natural Language Toolkit (NLTK), una popular biblioteca de Python para trabajar con datos de lenguaje humano.

### Instalación de NLTK

Antes de que podamos comenzar a codificar, necesitamos instalar NLTK. NLTK se puede instalar usando pip, un administrador de paquetes para Python:

```
pip install nltk
```

### descargando datos NLTK

Una vez que se instala NLTK, necesitamos descargar los datos que utilizará NLTK. Estos datos incluyen elementos como listas de palabras en inglés, reglas gramaticales, etc.

Podemos descargar estos datos usando el descargador NLTK:

```python
import nltk

nltk.download()
```

Esto abrirá una ventana donde podemos seleccionar qué datos descargar. Por ahora, solo descargaremos los datos "populares".

### Conceptos básicos de NLTK

Ahora que tenemos NLTK instalado y los datos descargados, podemos comenzar a jugar con algunas de las características de NLTK.

Primero, importemos la biblioteca NLTK:

```python
import nltk
```

A continuación, elijamos un texto con el que trabajar. NLTK viene con una serie de textos que podemos usar. Para este ejemplo, usaremos el corpus "gutenberg", que contiene varios libros clásicos:

```python
from nltk.corpus import gutenberg
```

Ahora que tenemos cargado el corpus de gutenberg, podemos acceder a los textos que contiene. Por ejemplo, para obtener el texto de "Alicia en el país de las maravillas" podemos hacer lo siguiente:

```python
alice = gutenberg.raw('carroll-alice.txt')
```

También podemos acceder a las palabras del texto:

```python
alice_words = gutenberg.words('carroll-alice.txt')
```

Y las oraciones:

```python
alice_sents = gutenberg.sents('carroll-alice.txt')
```

### Preprocesamiento de texto

Antes de que podamos hacer más análisis del texto, necesitamos preprocesarlo. Este paso de preprocesamiento incluye cosas como:

- Tokenización: Dividir el texto en palabras u oraciones individuales.

- Normalización: Convirtiendo las palabras a minúsculas y eliminando la puntuación.

- Stemming o lematización: reducción de una palabra a su forma base.

No entraremos en demasiados detalles sobre cada uno de estos pasos aquí, pero NLTK proporciona una serie de funciones que facilitan la realización de estos pasos de preprocesamiento.

Por ejemplo, para tokenizar un texto en oraciones, podemos usar la función ```sent_tokenize```:

```python
from nltk.tokenize import sent_tokenize

sentences = sent_tokenize(alice)
```

Para tokenizar un texto en palabras, podemos usar la función ```word_tokenize```:

```python
from nltk.tokenize import word_tokenize

words = word_tokenize(alice)
```

También podemos normalizar el texto convirtiéndolo a minúsculas y eliminando la puntuación:

```python
from nltk.tokenize import RegexpTokenizer

tokenizer = RegexpTokenizer(r'\w+')

words = tokenizer.tokenize(alice.lower())
```

Finalmente, podemos derivar o lematizar el texto. Stemming reduce una palabra a su forma base, p. "correr" se convierte en "correr". La lematización reduce una palabra a su forma básica, pero tiene en cuenta el contexto de la palabra, p. "running" se convierte en "run" pero "ran" se convierte en "run".

```python
from nltk.stem import PorterStemmer, WordNetLemmatizer

stemmer = PorterStemmer()
lemmatizer = WordNetLemmatizer()

stemmed_words = [stemmer.stem(w) for w in words]
lemmatized_words = [lemmatizer.lemmatize(w) for w in words]
```

### Etiquetado de parte del discurso

El etiquetado de parte del discurso (POS) es el proceso de asignar una etiqueta POS a cada palabra en un texto. Las etiquetas POS son etiquetas que indican la función gramatical de una palabra, p. si una palabra es un sustantivo, verbo, adjetivo, etc.

NLTK proporciona varios etiquetadores de POS diferentes, pero para este ejemplo, usaremos el etiquetador de POS predeterminado:

```python
from nltk import pos_tag

tagged_words = pos_tag(words)
```

La salida de la función ```pos_tag``` es una lista de tuplas, donde cada tupla consta de una palabra y su etiqueta POS.

### Reconocimiento de entidad nombrada

El reconocimiento de entidades nombradas (NER) es la tarea de identificar entidades nombradas en un texto, p. personas, lugares, organizaciones, etc.

NLTK proporciona varios etiquetadores NER diferentes, pero para este ejemplo, usaremos el etiquetador NER predeterminado:

```python
from nltk import ne_chunk

named_entities = ne_chunk(tagged_words)
```

La salida de la función ```ne_chunk``` es un árbol, donde cada nodo del árbol representa una entidad con nombre.

### Clasificación de texto

La clasificación de texto es la tarea de asignar una categoría o etiqueta a un fragmento de texto. Por ejemplo, podríamos querer clasificar un fragmento de texto como "positivo" o "negativo".

Hay varias formas diferentes de enfocar la clasificación de texto, pero para este ejemplo, usaremos un enfoque simple de bolsa de palabras.

Primero, crearemos una lista de palabras positivas y negativas:

```python
positive_words = ['good', 'great', 'awesome', 'fantastic', 'excellent']
negative_words = ['bad', 'terrible', 'horrible', 'awful', 'poor']
```

A continuación, contaremos el número de palabras positivas y negativas de nuestro texto:

```python
num_positive_words = 0
num_negative_words = 0

for word in words:
    if word in positive_words:
        num_positive_words += 1
    elif word in negative_words:
        num_negative_words += 1
```

Finalmente, clasificaremos el texto como positivo o negativo según el número de palabras positivas y negativas:

```python
if num_positive_words > num_negative_words:
    print('The text is positive.')
elif num_positive_words < num_negative_words:
    print('The text is negative.')
else:
    print('The text is neutral.')
```

Por supuesto, este es un enfoque muy simple para la clasificación de texto y, en la práctica, usaríamos métodos más sofisticados.

## Recursos para lecturas adicionales

- [Procesamiento del lenguaje natural con Python](http://www.nltk.org/book/) - Una guía completa y práctica de PNL en Python.

- [Python para NLP: tokenización, derivación y lematización] (https://www.datacamp.com/community/tutorials/stemming-lemmatization-python) - Un tutorial sobre cómo realizar el preprocesamiento de texto en Python.

- [Reconocimiento de entidad con nombre con NLTK] (https://towardsdatascience.com/named-entity-recognition-with-nltk-d0a87a1544f1) - Un tutorial sobre cómo realizar NER en Python usando NLTK.

- [Clasificación de texto con NLTK](https://towardsdatascience.com/text-classification-with-nltk-d0a87a1544f1) - Un tutorial sobre cómo realizar la clasificación de texto en Python usando NLTK.