---
title: 099: Creación de agentes de aprendizaje por refuerzo en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T06:18:09.779Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:18:08.153Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [099: Building Reinforcement Learning Agents in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/099-building-reinforcement-learning-agents-in-tensorflow-js-and-node-js)
{.links-list}


## 099: Creación de agentes de aprendizaje por refuerzo en TensorFlow.js y Node.js

En esta publicación, aprenderemos a crear agentes de aprendizaje por refuerzo en TensorFlow.js y Node.js. Comenzaremos cubriendo brevemente los conceptos básicos del aprendizaje por refuerzo. Luego veremos cómo instalar TensorFlow.js y sus dependencias. Finalmente, escribiremos un script simple de Node.js que entrene a un agente de aprendizaje por refuerzo para jugar un juego simple.

### ¿Qué es el aprendizaje por refuerzo?

El aprendizaje por refuerzo es un tipo de aprendizaje automático que permite a los agentes aprender realizando acciones en un entorno y recibiendo recompensas por sus acciones. El objetivo del aprendizaje por refuerzo es maximizar la recompensa total que recibe el agente.

Hay dos tipos principales de aprendizaje por refuerzo:

- **Aprendizaje por refuerzo discreto**: En este tipo de aprendizaje por refuerzo, el agente solo puede realizar un número finito de acciones.
- **Aprendizaje por refuerzo continuo**: En este tipo de aprendizaje por refuerzo, el agente puede realizar una infinidad de acciones.

En esta publicación, nos centraremos en el aprendizaje por refuerzo discreto.

### Configuración de TensorFlow.js y sus dependencias

Antes de que podamos comenzar a crear agentes de aprendizaje por refuerzo, debemos instalar TensorFlow.js y sus dependencias.

Primero, necesitamos instalar Node.js. Node.js es un tiempo de ejecución de JavaScript que nos permite ejecutar código JavaScript fuera de un navegador web.

En segundo lugar, necesitamos instalar la API TensorFlow.js Node.js. La API TensorFlow.js Node.js nos permite usar TensorFlow.js en un entorno Node.js.

Tercero, necesitamos instalar la biblioteca de aprendizaje de refuerzo para TensorFlow.js. La biblioteca de aprendizaje por refuerzo para TensorFlow.js nos permite crear agentes de aprendizaje por refuerzo en TensorFlow.js.

Cuarto, necesitamos instalar un motor de juego. En esta publicación, usaremos el motor de juego simple. Simple Game Engine es un motor de juego ligero que facilita el desarrollo y la prueba de agentes de aprendizaje por refuerzo.

Finalmente, necesitamos instalar un editor de texto. En esta publicación, usaremos Visual Studio Code. Visual Studio Code es un editor de texto gratuito y de código abierto de Microsoft.

### Escritura de un script de Node.js que entrena a un agente de aprendizaje por refuerzo

Ahora que tenemos instalado TensorFlow.js y sus dependencias, podemos escribir un script de Node.js que entrene a un agente de aprendizaje por refuerzo.

Primero, necesitamos requerir las dependencias que instalamos. Necesitamos la API TensorFlow.js Node.js, la biblioteca de aprendizaje de refuerzo para TensorFlow.js y el motor de juego simple.

```javascript
const tf = require('@tensorflow/tfjs-node');
const rl = require('@tensorflow-models/rl');
const { SimpleGameEngine } = require('simple-game-engine');
```

A continuación, debemos definir el juego que jugará el agente. Hacemos esto creando una nueva instancia de la clase SimpleGameEngine.

```javascript
const game = new SimpleGameEngine();
```

La clase SimpleGameEngine tiene una serie de métodos que podemos usar para definir el juego. En este ejemplo, usaremos el método addEntity() para agregar un jugador al juego.

```javascript
game.addEntity({
  id: 'player',
  x: 0,
  y: 0,
  width: 10,
  height: 10
});
```

También podemos usar el método addEntity() para agregar obstáculos al juego.

```javascript
game.addEntity({
  id: 'obstacle1',
  x: 50,
  y: 50,
  width: 10,
  height: 10
});

game.addEntity({
  id: 'obstacle2',
  x: 100,
  y: 100,
  width: 10,
  height: 10
});
```

Ahora que hemos definido el juego, necesitamos definir las reglas del juego. En este ejemplo, el objetivo del juego es evitar los obstáculos y llegar al final del nivel. El nivel tiene 50 unidades de ancho y el jugador comienza en el lado izquierdo del nivel. El jugador puede moverse hacia la izquierda, derecha, arriba o abajo. Si el jugador choca con un obstáculo, el juego termina. Si el jugador llega al lado derecho del nivel, el juego termina y el jugador recibe una recompensa de 100.

```javascript
game.setRules({
  win: ['atXPos', 'player', 50],
  lose: ['collides', 'player', ['obstacle1', 'obstacle2']],
  endOnWin: true
});
```

También podemos usar el método setRules() para definir otras reglas para el juego. Por ejemplo, podríamos usar el método setRules() para definir un límite de tiempo para el juego.

Ahora que hemos definido el juego, necesitamos definir el entorno. El entorno es la interfaz entre el agente y el juego. En este ejemplo, usaremos la clase SimpleGameEngineEnvironment de la biblioteca de aprendizaje por refuerzo para TensorFlow.js.

```javascript
const environment = new rl.SimpleGameEngineEnvironment(game);
```

La clase SimpleGameEngineEnvironment tiene una serie de métodos que podemos usar para interactuar con el entorno. En este ejemplo, usaremos el método reset() para restablecer el entorno y el método step() para dar un paso en el entorno.

```javascript
environment.reset();

while (!environment.isDone()) {
  const action = environment.actionSpace.sample();
  environment.step(action);
}
```

La propiedad actionSpace es un espacio que contiene todas las posibles acciones que puede realizar el agente. En este ejemplo, usamos el método sample() para muestrear aleatoriamente una acción del espacio de acción.

Ahora que hemos definido el entorno, necesitamos definir el agente. El agente es el algoritmo de aprendizaje por refuerzo que usaremos para entrenar al agente. En este ejemplo, usaremos el método DQN() de la biblioteca de aprendizaje por refuerzo para TensorFlow.js.

```javascript
const agent = new rl.DQN({
  environment,
  numEpisodes: 100,
  trainInterval: 10
});
```

El método DQN() toma varias opciones como argumentos. En este ejemplo, usamos la opción numEpisodes para especificar el número de episodios para los que queremos que se entrene el agente. También usamos la opción trainInterval para especificar el intervalo en el que queremos que el agente entrene.

Ahora que hemos definido el agente, necesitamos entrenarlo. Hacemos esto llamando al método train() en el agente.

```javascript
agent.train();
```

Una vez que el agente ha sido entrenado, podemos usar el método save() para guardar el agente entrenado.

```javascript
agent.save('path/to/agent');
```

También podemos usar el método load() para cargar un agente entrenado.

```javascript
agent.load('path/to/agent');
```

### Conclusión

En esta publicación, aprendimos cómo crear agentes de aprendizaje por refuerzo en TensorFlow.js y Node.js. Hemos visto cómo instalar TensorFlow.js y sus dependencias. También escribimos un script simple de Node.js que entrena a un agente de aprendizaje por refuerzo para que juegue un juego simple.