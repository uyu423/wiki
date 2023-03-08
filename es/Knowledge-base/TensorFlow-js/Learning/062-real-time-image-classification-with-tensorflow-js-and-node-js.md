---
title: 062: Clasificación de imágenes en tiempo real con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T21:36:45.222Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:36:43.517Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [062: Real-Time Image Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/062-real-time-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# Clasificación de imágenes en tiempo real con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear una aplicación de clasificación de imágenes en tiempo real con TensorFlow.js y Node.js.

TensorFlow.js es una poderosa herramienta para crear modelos de aprendizaje automático en JavaScript. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar JavaScript en el servidor.

 Juntas, estas dos tecnologías se pueden utilizar para crear potentes aplicaciones de clasificación de imágenes en tiempo real.

## Instalación de TensorFlow.js

El primer paso es instalar TensorFlow.js. Puede hacer esto usando el Administrador de paquetes de nodos (NPM):

```
npm install @tensorflow/tfjs
```

## Instalación de Node.js

Si aún no tiene Node.js instalado, puede hacerlo siguiendo las instrucciones en el sitio web de Node.js: https://nodejs.org/en/

## Construyendo el modelo

Ahora que tenemos instalados TensorFlow.js y Node.js, podemos comenzar a construir nuestro modelo de clasificación de imágenes.

Usaremos el modelo MobileNet. MobileNet es un modelo preentrenado que ha sido entrenado en un gran conjunto de datos de imágenes.

Para usar el modelo MobileNet, primero debemos cargarlo en TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');

const mobilenet = require('@tensorflow-models/mobilenet');

async function loadModel() {
  const model = await mobilenet.load();
  return model;
}
```

Una vez cargado el modelo, podemos usarlo para clasificar imágenes.

La siguiente función classifyImage() toma una imagen como entrada y devuelve las 5 predicciones principales:

```javascript
async function classifyImage(image) {
  const model = await loadModel();
  const predictions = await model.classify(image);
  return predictions;
}
```

## Sirviendo al modelo

Ahora que tenemos nuestro modelo de clasificación de imágenes construido, necesitamos servirlo usando Node.js.

Usaremos el marco web Express. Express es un marco web popular para Node.js.

Para instalar Express, ejecute el siguiente comando:

```
npm install express
```

Una vez instalado Express, podemos crear un archivo llamado server.js y agregar el siguiente código:

```javascript
const express = require('express');
const app = express();

app.use(express.static('public'));

app.get('/classify', async (req, res) => {
  const image = req.query.image;
  const predictions = await classifyImage(image);
  res.json(predictions);
});

app.listen(3000, () => console.log('Server listening on port 3000!'));
```

El código anterior hace lo siguiente:

- Sirve archivos estáticos desde el directorio público
- Crea un punto final (/classify) que toma una URL de imagen como parámetro de consulta
- Utiliza la función classifyImage() para clasificar la imagen
- Devuelve las 5 mejores predicciones como JSON

## Construyendo el front-end

Ahora que tenemos nuestro servidor Node.js en funcionamiento, podemos comenzar a construir el front-end de nuestra aplicación.

Usaremos React. React es una biblioteca de JavaScript popular para crear interfaces de usuario.

Para instalar React, ejecute el siguiente comando:

```
npm install react react-dom
```

Una vez instalado React, podemos crear un archivo llamado App.js y agregar el siguiente código:

```javascript
import React, { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [image, setImage] = useState(null);
  const [predictions, setPredictions] = useState([]);

  useEffect(() => {
    async function fetchPredictions() {
      const response = await fetch('/classify?image=' + image);
      const predictions = await response.json();
      setPredictions(predictions);
    }
    if (image) {
      fetchPredictions();
    }
  }, [image]);

  const onSelectFile = e => {
    if (e.target.files && e.target.files.length > 0) {
      const reader = new FileReader();
      reader.onload = () => setImage(reader.result);
      reader.readAsDataURL(e.target.files[0]);
    }
  };

  return (
    <div className="App">
      <h1>Real-Time Image Classification</h1>
      <p>
        Select an image to classify:
      </p>
      <input type="file" accept="image/*" onChange={onSelectFile} />
      {predictions.length > 0 && (
        <div className="predictions">
          <h2>Predictions</h2>
          {predictions.map((prediction, i) => (
            <div key={i}>
              <div className="prediction-label">{prediction.className}</div>
              <div className="prediction-confidence">{prediction.probability.toFixed(2)}</div>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

export default App;
```

El código anterior hace lo siguiente:

- Representa un campo de entrada de archivo que permite al usuario seleccionar una imagen
- Cuando se selecciona una imagen, la imagen se carga en el servidor y se obtienen las predicciones
- Las predicciones se muestran en la página.

## Ejecutar la aplicación

Ahora que tenemos nuestro código de front-end y back-end completo, podemos ejecutar la aplicación.

Primero, inicie el servidor Node.js ejecutando el siguiente comando:

```
node server.js
```

Luego, abra la siguiente URL en su navegador: http://localhost:3000

¡Ahora debería ver la aplicación de clasificación de imágenes en funcionamiento!