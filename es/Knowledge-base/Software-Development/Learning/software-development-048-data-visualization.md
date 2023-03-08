---
title: Desarrollo de Software 048: Visualización de Datos
description: 
published: true
date: 2023-02-11T17:55:54.664Z
tags: 
editor: markdown
dateCreated: 2023-02-11T17:55:52.967Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 048: Data Visualization***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-048-data-visualization)
{.links-list}


# Desarrollo de Software 048: Visualización de Datos

El proceso de visualización de datos es clave para comprender las complejas relaciones que existen dentro de los conjuntos de datos. Al visualizar datos, podemos obtener información que, de otro modo, estaría oculta.

La visualización de datos es un proceso de transformación de datos a un formato gráfico. Esto se puede hacer usando una variedad de métodos, incluyendo tablas, gráficos y mapas.

Hay muchas razones por las que la visualización de datos es importante. Nos puede ayudar a:

- Comprender conjuntos de datos complejos
- Encuentra tendencias y patrones.
- Comunicar datos de manera efectiva.
- Tomar mejores decisiones

La visualización de datos es una herramienta poderosa que debe usarse en cada etapa del proceso de análisis de datos. En esta publicación, veremos algunos de los conceptos básicos de la visualización de datos. Aprenderemos a crear tablas y gráficos utilizando el lenguaje de programación R.

## Introducción a la visualización de datos

Antes de que podamos comenzar a visualizar datos, necesitamos tener algunos datos con los que trabajar. Para esta publicación, utilizaremos el conjunto de datos integrado de R `mtcars`. Este conjunto de datos contiene información sobre diferentes marcas y modelos de automóviles.

Para cargar el conjunto de datos, usaremos la función `data()`:

```r
data("mtcars")
```

Una vez que se carga el conjunto de datos, podemos echarle un vistazo usando la función `head()`:

```r
head(mtcars)
```

## Creación de tablas y gráficos

Hay muchos tipos diferentes de tablas y gráficos que se pueden usar para visualizar datos. El tipo de cuadro o gráfico que utilice dependerá del tipo de datos con los que esté trabajando y del mensaje que desee comunicar.

Algunos de los tipos más comunes de tablas y gráficos son:

- Gráfica de barras
- Gráficos de líneas
- Gráficos circulares
- Gráfico de dispersión

En esta sección, veremos cómo crear algunos de estos tipos de gráficos comunes usando R.

### Gráfica de barras

Los gráficos de barras son uno de los tipos de gráficos más comunes. A menudo se utilizan para comparar puntos de datos.

Para crear un gráfico de barras en R, podemos usar la función `barplot()`:

```r
barplot(mtcars$mpg)
```

![](https://i.imgur.com/5YU8F1v.png)

También podemos usar la función `barplot()` para comparar múltiples puntos de datos. Por ejemplo, podemos comparar el mpg de diferentes marcas de automóviles:

```r
barplot(mtcars$mpg, mtcars$brand)
```

![](https://i.imgur.com/VkzM4jK.png)

### Gráficos de líneas

Los gráficos de líneas son otro tipo común de gráfico. A menudo se utilizan para visualizar datos a lo largo del tiempo.

Para crear un gráfico de líneas en R, podemos usar la función `plot()`:

```r
plot(mtcars$mpg)
```

![](https://i.imgur.com/tR3y7Nb.png)

También podemos usar la función `plot()` para comparar múltiples puntos de datos. Por ejemplo, podemos comparar el mpg de diferentes marcas de automóviles:

```r
plot(mtcars$mpg, mtcars$brand)
```

![](https://i.imgur.com/VkzM4jK.png)

### Gráficos circulares

Los gráficos circulares son un tipo de gráfico que se utiliza para visualizar datos como una proporción de un todo.

Para crear un gráfico circular en R, podemos usar la función `pie()`:

```r
pie(mtcars$mpg)
```

![](https://i.imgur.com/9nHZ8N4.png)

También podemos usar la función `pie()` para comparar múltiples puntos de datos. Por ejemplo, podemos comparar el mpg de diferentes marcas de automóviles:

```r
pie(mtcars$mpg, mtcars$brand)
```

![](https://i.imgur.com/9nHZ8N4.png)

### Gráfico de dispersión

Los diagramas de dispersión son un tipo de gráfico que se utiliza para visualizar la relación entre dos variables numéricas.

Para crear un diagrama de dispersión en R, podemos usar la función `plot()`:

```r
plot(mtcars$mpg, mtcars$hp)
```

![](https://i.imgur.com/F3Yr5jM.png)

También podemos usar la función `plot()` para comparar múltiples puntos de datos. Por ejemplo, podemos comparar el mpg de diferentes marcas de automóviles:

```r
plot(mtcars$mpg, mtcars$brand)
```

![](https://i.imgur.com/VkzM4jK.png)

## Personalización de tablas y gráficos

Una vez que haya creado un cuadro o gráfico básico, es probable que desee personalizarlo para comunicar mejor sus datos. Hay muchas opciones diferentes para personalizar tablas y gráficos en R.

Algunas de las opciones que tal vez quieras considerar son:

- Agregar títulos
- Agregar etiquetas
- Cambio de colores
- Cambio de tipos de línea
- Agregar una leyenda

En esta sección, veremos cómo personalizar algunos de los cuadros y gráficos que creamos en la sección anterior.

### Adición de títulos

Agregar un título a un cuadro o gráfico puede ayudar a comunicar el mensaje de los datos de manera más efectiva.

Para agregar un título a un cuadro o gráfico en R, podemos usar la función `title()`:

```r
title("Miles per gallon by car brand")
```

![](https://i.imgur.com/VkzM4jK.png)

### Adición de etiquetas

Agregar etiquetas a un cuadro o gráfico puede ayudar a que los datos sean más comprensibles.

Para agregar etiquetas a un cuadro o gráfico en R, podemos usar las funciones `xlab()` y `ylab()`:

```r
xlab("Car brand")
ylab("Miles per gallon")
```

![](https://i.imgur.com/VkzM4jK.png)

### Cambio de colores

Cambiar los colores de un cuadro o gráfico puede ayudar a que los datos sean más atractivos visualmente.

Para cambiar los colores de un cuadro o gráfico en R, podemos usar el argumento `col`:

```r
barplot(mtcars$mpg, mtcars$brand, col = "red")
```

![](https://i.imgur.com/VkzM4jK.png)

### Cambio de tipos de línea

Cambiar los tipos de línea de un cuadro o gráfico puede ayudar a que los datos sean más atractivos visualmente.

Para cambiar los tipos de línea de un cuadro o gráfico en R, podemos usar el argumento `lty`:

```r
plot(mtcars$mpg, mtcars$hp, lty = "dotted")
```

![](https://i.imgur.com/F3Yr5jM.png)

### Adición de una leyenda

Agregar una leyenda a un cuadro o gráfico puede ayudar a que los datos sean más comprensibles.

Para agregar una leyenda a un cuadro o gráfico en R, podemos usar la función `legend()`:

```r
legend("topright", mtcars$brand, cex = 0.5)
```

![](https://i.imgur.com/VkzM4jK.png)

## Conclusión

En esta publicación, hemos aprendido sobre los conceptos básicos de la visualización de datos. Hemos aprendido a crear tablas y gráficos utilizando el lenguaje de programación R. También hemos aprendido a personalizar tablas y gráficos para comunicar mejor nuestros datos.