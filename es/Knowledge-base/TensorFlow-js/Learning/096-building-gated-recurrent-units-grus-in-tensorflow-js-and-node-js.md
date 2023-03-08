---
title: 096: Creación de unidades recurrentes cerradas (GRU) en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T05:38:01.293Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:37:59.464Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [096: Building Gated Recurrent Units (GRUs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/096-building-gated-recurrent-units-grus-in-tensorflow-js-and-node-js)
{.links-list}


# GRU en TensorFlow.js y Node.js

## ¿Qué son las GRU?

Las unidades recurrentes cerradas (GRU) son un tipo de red neuronal recurrente (RNN) que se han diseñado para capturar mejor las dependencias a largo plazo en datos secuenciales. A diferencia de las RNN tradicionales, las GRU tienen dos puertas que controlan el flujo de información hacia y desde el estado oculto. La puerta de actualización decide la cantidad de información nueva que se debe dejar entrar, mientras que la puerta de reinicio decide la cantidad de información antigua que se debe olvidar.

## Construyendo una GRU en TensorFlow.js

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador y en Node.js. En este tutorial, veremos cómo crear una GRU en TensorFlow.js y usarla para predecir la siguiente palabra en una secuencia.

### Instalación de TensorFlow.js

Si está ejecutando este tutorial en el navegador, puede instalar TensorFlow.js usando la siguiente etiqueta de secuencia de comandos:

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>
```

Si está ejecutando este tutorial en Node.js, puede instalar TensorFlow.js con el siguiente comando:

```
npm install @tensorflow/tfjs
```

### Cargando los datos

Usaremos un conjunto de datos de reseñas de productos de Amazon para este tutorial. El conjunto de datos contiene reseñas de diferentes productos, junto con una calificación de estrellas para cada reseña.

Primero necesitaremos cargar el conjunto de datos en TensorFlow.js. Podemos hacer esto usando la función `tf.data.csv`:

```
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/amazon_reviews_multilingual_CSV_V2/reviews.csv', {
  columnConfigs: {
    review_body: {
      isLabel: true
    },
    review_title: {
      isLabel: true
    },
    star_rating: {
      isLabel: true
    }
  }
});
```

### Preprocesamiento de los datos

Necesitamos preprocesar los datos antes de poder entrenar nuestro modelo. Tendremos que hacer los siguientes pasos de preprocesamiento:

- Tokenizar las reseñas en oraciones.
- Tokenizar las oraciones en palabras.
- Convertir las palabras en números enteros.

Podemos usar las funciones `tf.tokenize` y `tf.tensorize` para tokenizar y convertir las reseñas en números enteros, respectivamente.

```
const sentences = dataset.map(({review_body, review_title}) => tf.tokenize(review_body + ' ' + review_title));

const words = sentences.map(sentence => tf.tensor1d(sentence, 'int32'));
```

### Construyendo el modelo

Ahora estamos listos para construir nuestro modelo. Usaremos una GRU para este tutorial. La primera capa de nuestro modelo será una capa `Embedding`. Esta capa tomará nuestras palabras y las convertirá en vectores de un tamaño específico. Podemos especificar el tamaño de los vectores usando los parámetros `inputDim` y `outputDim`. También necesitaremos especificar el parámetro `maskZero`, que le dice a la capa que ignore las palabras con un valor de 0 (es decir, relleno).

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

La siguiente capa en nuestro modelo será la capa GRU. Esta capa tomará los vectores de salida de la capa `Embedding` y los convertirá en un solo vector que captura la información en la secuencia. Podemos especificar el tamaño del estado oculto usando el parámetro `unidades`.

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

La capa final de nuestro modelo será una capa `Densa`. Esta capa tomará el vector de salida de la capa GRU y lo convertirá en una distribución de probabilidad sobre las palabras de nuestro vocabulario. Podemos especificar el número de unidades en la capa usando el parámetro `unidades`. También necesitaremos especificar los parámetros `activación` y `kernelInitializer`. El parámetro `activación` especifica la función de activación a usar, mientras que el parámetro `kernelInitializer` especifica el inicializador para los pesos de la capa.

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### Compilando el modelo

Antes de que podamos entrenar nuestro modelo, necesitamos compilarlo. Necesitamos especificar los siguientes parámetros al compilar el modelo:

- El optimizador a utilizar. Usaremos el optimizador `adam` para este tutorial.
- La función de pérdida a utilizar. Usaremos la función de pérdida `categoricalCrossentropy` para este tutorial.
- Las métricas a seguir. Realizaremos un seguimiento de la métrica de "precisión" para este tutorial.

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### Entrenando al modelo

Ahora estamos listos para entrenar nuestro modelo. Podemos hacer esto usando el método `model.fit`. Tendremos que especificar los siguientes parámetros al entrenar el modelo:

- Los datos de entrenamiento. Este debería ser un objeto `tf.data.Dataset`.
- El número de épocas para entrenar. Estaremos entrenando durante 10 épocas para este tutorial.
- El tamaño del lote a utilizar. Usaremos un tamaño de lote de 32 para este tutorial.

También podemos especificar un parámetro `validationData`. Este debe ser un objeto `tf.data.Dataset` que contenga los datos de validación. Si especificamos un parámetro `validationData`, el modelo se evaluará en los datos de validación al final de cada época.

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### Haciendo predicciones

Podemos usar nuestro modelo entrenado para hacer predicciones sobre nuevos datos. Tendremos que tokenizar y convertir los nuevos datos en números enteros antes de poder hacer predicciones. Podemos usar las funciones `tf.tokenize` y `tf.tensorize` para hacer esto:

```
const newSentences = tf.tokenize('this is a new sentence');
const newWords = tf.tensor1d(newSentences, 'int32');
```

Luego podemos usar el método `model.predict` para hacer predicciones sobre los nuevos datos:

```
model.predict(newWords).print();
```

## Construyendo una GRU en Node.js

En esta sección, veremos cómo crear una GRU en Node.js. Usaremos el mismo conjunto de datos de revisión de productos de Amazon que en la sección anterior.

### Instalando las dependencias

Tendremos que instalar las siguientes dependencias antes de que podamos comenzar a codificar:

- `@tensorflow/tfjs-node`: estos son los enlaces de TensorFlow.js Node.js.
- `csv-parser`: este es un analizador CSV para Node.js.
- `tokenizer`: Esta es una biblioteca de procesamiento de lenguaje natural para Node.js.

Podemos instalar estas dependencias usando el siguiente comando:

```
npm install @tensorflow/tfjs-node csv-parser tokenizer
```

### Cargando los datos

Comenzaremos cargando el conjunto de datos en la memoria. Podemos hacer esto usando la biblioteca `csv-parser`:

```
const parser = csvParser();

parser.on('data', (data) => {
  // do something with the data
});

parser.on('end', () => {
  // do something when the parsing is finished
});

fs.createReadStream('reviews.csv').pipe(parser);
```

### Preprocesamiento de los datos

Necesitamos preprocesar los datos antes de poder entrenar nuestro modelo. Tendremos que hacer los siguientes pasos de preprocesamiento:

- Tokenizar las reseñas en oraciones.
- Tokenizar las oraciones en palabras.
- Convertir las palabras en números enteros.

Podemos usar la biblioteca `tokenizer` para tokenizar las reseñas en oraciones y palabras. Luego podemos usar la función `tf.tensor1d` para convertir las palabras en números enteros:

```
const sentences = reviews.map((review) => tokenizer.sentences(review));

const words = sentences.map((sentence) => tf.tensor1d(sentence.map((word) => tokenizer.words(word))));
```

### Construyendo el modelo

Ahora estamos listos para construir nuestro modelo. Usaremos una GRU para este tutorial. La primera capa de nuestro modelo será una capa `Embedding`. Esta capa tomará nuestras palabras y las convertirá en vectores de un tamaño específico. Podemos especificar el tamaño de los vectores usando los parámetros `inputDim` y `outputDim`. También necesitaremos especificar el parámetro `maskZero`, que le dice a la capa que ignore las palabras con un valor de 0 (es decir, relleno).

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

La siguiente capa en nuestro modelo será la capa GRU. Esta capa tomará los vectores de salida de la capa `Embedding` y los convertirá en un solo vector que captura la información en la secuencia. Podemos especificar el tamaño del estado oculto usando el parámetro `unidades`.

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

La capa final de nuestro modelo será una capa `Densa`. Esta capa tomará el vector de salida de la capa GRU y lo convertirá en una distribución de probabilidad sobre las palabras de nuestro vocabulario. Podemos especificar el número de unidades en la capa usando el parámetro `unidades`. También necesitaremos especificar los parámetros `activación` y `kernelInitializer`. El parámetro `activación` especifica la función de activación a usar, mientras que el parámetro `kernelInitializer` especifica el inicializador para los pesos de la capa.

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### Compilando el modelo

Antes de que podamos entrenar nuestro modelo, necesitamos compilarlo. Necesitamos especificar los siguientes parámetros al compilar el modelo:

- El optimizador a utilizar. Usaremos el optimizador `adam` para este tutorial.
- La función de pérdida a utilizar. Usaremos la función de pérdida `categoricalCrossentropy` para este tutorial.
- Las métricas a seguir. Realizaremos un seguimiento de la métrica de "precisión" para este tutorial.

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### Entrenando al modelo

Ahora estamos listos para entrenar nuestro modelo. Podemos hacer esto usando el método `model.fit`. Tendremos que especificar los siguientes parámetros al entrenar el modelo:

- Los datos de entrenamiento. Este debería ser un objeto `tf.data.Dataset`.
- El número de épocas para entrenar. Estaremos entrenando durante 10 épocas para este tutorial.
- El tamaño del lote a utilizar. Usaremos un tamaño de lote de 32 para este tutorial.

También podemos especificar un parámetro `validationData`. Este debe ser un objeto `tf.data.Dataset` que contenga los datos de validación. Si especificamos un parámetro `validationData`, el modelo se evaluará en los datos de validación al final de cada época.

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### Haciendo predicciones

Podemos usar nuestro modelo entrenado para hacer predicciones sobre nuevos datos. Tendremos que tokenizar y convertir los nuevos datos en números enteros antes de poder hacer predicciones. Podemos usar las bibliotecas `tokenizer` y `tf.tensor1d` para hacer esto:

```
const newSentences = tokenizer.sentences('this is a new sentence');
const newWords = tf.tensor1d(newSentences.map((sentence) => tokenizer.words(sentence)));
```

Luego podemos usar el método `model.predict` para hacer predicciones sobre los nuevos datos:

```
model.predict(newWords).print();
```

## Recursos

- [Unidades recurrentes cerradas] (https://en.wikipedia.org/wiki/Gated_recurrent_unit)
- [TensorFlow.js](https://js.tensorflow.org/)
- [TensorFlow.js para Node.js](https://js.tensorflow.org/api/latest/# tensorflowjs_node)
- [csv-parser](https://www.npmjs.com/package/csv-parser)
- [tokenizador](https://www.npmjs.com/package/tokenizer)