---
title: Pandas
description: 
published: true
date: 2023-02-02T02:23:55.264Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:23:50.546Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Pandas***English** document is available*](/en/Knowledge-base/Dictionary/pandas)
{.links-list}


# Descripción general

Pandas es una potente y popular biblioteca de manipulación y análisis de datos de código abierto para Python. Se utiliza para la disputa de datos, la limpieza de datos, la visualización de datos y otras tareas relacionadas con los datos. Pandas es una herramienta muy versátil y eficiente para trabajar con grandes conjuntos de datos y se puede utilizar para analizar y manipular datos de forma rápida y sencilla. También se utiliza para análisis estadístico y aprendizaje automático.

# Descripción

Pandas es una potente y popular biblioteca de manipulación y análisis de datos de código abierto para Python. Se utiliza para la disputa de datos, la limpieza de datos, la visualización de datos y otras tareas relacionadas con los datos. Pandas es una herramienta muy versátil y eficiente para trabajar con grandes conjuntos de datos y se puede utilizar para analizar y manipular datos de forma rápida y sencilla. También se utiliza para análisis estadístico y aprendizaje automático.

Pandas se basa en la biblioteca NumPy, que proporciona una poderosa variedad de herramientas para el cálculo numérico. Pandas proporciona una amplia gama de estructuras de datos y operaciones para manipular datos numéricos, como marcos de datos, series y paneles. También proporciona potentes funciones para la agregación y manipulación de datos.

Pandas es fácil de usar y tiene una API simple. Tiene una amplia gama de características que facilitan el trabajo con grandes conjuntos de datos, como la disputa de datos, la limpieza de datos, la visualización de datos y el análisis de datos. También proporciona potentes funciones para la manipulación de datos, como filtrado, clasificación y combinación.

Pandas también proporciona potentes funciones para el análisis de datos, como el análisis estadístico y el aprendizaje automático. Tiene una amplia gama de funciones para el análisis de datos, como regresión lineal, agrupación de k-medias y árboles de decisión.

# Historia

Pandas fue creado en 2008 por Wes McKinney, un ingeniero de software estadounidense. Estaba frustrado con la falta de herramientas para el análisis y la manipulación de datos en Python y quería crear una herramienta que facilitara el trabajo con grandes conjuntos de datos.

Pandas se lanzó inicialmente en 2009 y desde entonces se ha convertido en una de las bibliotecas de manipulación y análisis de datos más populares para Python. Ahora lo utilizan miles de científicos de datos y desarrolladores de todo el mundo.

# Características

Pandas proporciona una amplia gama de funciones para la manipulación, el análisis y la visualización de datos. Tiene potentes funciones para la disputa de datos, la limpieza de datos, la visualización de datos y el análisis de datos. También proporciona potentes funciones para la manipulación de datos, como filtrado, clasificación y combinación.

Pandas también proporciona potentes funciones para el análisis de datos, como el análisis estadístico y el aprendizaje automático. Tiene una amplia gama de funciones para el análisis de datos, como regresión lineal, agrupación de k-medias y árboles de decisión.

Pandas también proporciona potentes funciones para la visualización de datos, como bibliotecas de trazado y visualización. Tiene una amplia gama de bibliotecas de trazado y visualización, como matplotlib, seaborn y plotly.

# Ejemplo

Veamos un ejemplo de cómo usar Pandas para analizar un conjunto de datos. Usaremos el popular conjunto de datos de Iris, que contiene información sobre los diferentes tipos de flores de Iris. Usaremos Pandas para analizar el conjunto de datos y descubrir qué tipo de Iris es el más popular.

Primero, importaremos la biblioteca de Pandas y el conjunto de datos de Iris.

```python
import pandas as pd
iris = pd.read_csv('iris.csv')
```

Ahora, usaremos Pandas para analizar el conjunto de datos. Usaremos la función `groupby()` para agrupar los datos por el tipo de flor de iris.

```python
iris_grouped = iris.groupby('species')
```

Finalmente, usaremos la función `count()` para contar el número de cada tipo de flor de iris en el conjunto de datos.

```python
iris_counts = iris_grouped.count()
```

Los resultados muestran que el tipo de flor de Iris más popular es la Setosa, con 50 muestras en el conjunto de datos.

# Pros y contras

Ventajas:

- Fácil de usar y tiene una API simple
- Potentes funciones para la disputa de datos, la limpieza de datos, la visualización de datos y el análisis de datos
- Potentes funciones para la manipulación de datos, como filtrado, clasificación y fusión
- Funciones potentes para el análisis de datos, como el análisis estadístico y el aprendizaje automático
- Amplia gama de bibliotecas de trazado y visualización.

Contras:

- Puede ser lento cuando se trabaja con grandes conjuntos de datos
- Soporte limitado para otros idiomas
- Soporte limitado para computación distribuida

# Controversia

No hay gran controversia en torno a Pandas. Es ampliamente aceptado como una de las bibliotecas de manipulación y análisis de datos más populares y poderosas para Python.

# Tecnología relacionada

Pandas está estrechamente relacionado con otras bibliotecas de análisis y manipulación de datos para Python, como NumPy, SciPy y Scikit-learn. También está relacionado con otras bibliotecas de análisis y manipulación de datos de código abierto, como R y Julia.

# Digresión

Pandas se ha convertido en una herramienta popular para el análisis y la manipulación de datos en Python. Es utilizado por miles de científicos de datos y desarrolladores de todo el mundo.

# Otros

Pandas es una biblioteca de código abierto, lo que significa que cualquiera puede contribuir a su desarrollo. Sus desarrolladores también lo mantienen activamente, lo que garantiza que esté actualizado con las últimas tendencias y tecnologías.