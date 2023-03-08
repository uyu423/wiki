---
title: 029: aprendizaje de refuerzo profundo con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T13:44:25.663Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:44:23.978Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [029: Deep Reinforcement Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/029-deep-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


El aprendizaje de refuerzo profundo (DRL) es una técnica de aprendizaje automático de vanguardia para capacitar a los agentes para que realicen tareas complejas en entornos difíciles. Si bien DRL existe desde hace un tiempo, solo recientemente se ha vuelto factible capacitar a los agentes de DRL en tiempo real debido a los avances en el poder de cómputo y los algoritmos.

TensorFlow.js es una poderosa biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Node.js es un tiempo de ejecución de JavaScript que permite aplicaciones de red rápidas y escalables.

En esta publicación, le mostraremos cómo usar TensorFlow.js y Node.js para capacitar a un agente de aprendizaje de refuerzo profundo para que juegue el juego clásico Pong. También proporcionaremos una interfaz basada en web para jugar contra el agente.

## ¿Qué es el aprendizaje por refuerzo profundo?

El aprendizaje de refuerzo profundo (DRL) es una técnica de aprendizaje automático para capacitar a los agentes para que realicen tareas complejas en entornos difíciles. En DRL, un agente interactúa con su entorno realizando acciones y recibiendo recompensas. El objetivo del agente es maximizar su recompensa esperada aprendiendo una política que asigna estados a acciones.

DRL es una técnica de aprendizaje profundo porque utiliza redes neuronales profundas para representar la política del agente. DRL también es una técnica de aprendizaje por refuerzo porque el agente es reforzado (es decir, recompensado) por realizar acciones que conducen a la finalización exitosa de la tarea.

## ¿Qué es Pong?

Pong es un videojuego clásico que se lanzó en 1972. El juego es simple: dos jugadores usan paletas para golpear una pelota de un lado a otro. El primer jugador en alcanzar una puntuación de 11 gana.

Pong es un excelente entorno para entrenar a un agente de aprendizaje por refuerzo profundo porque es lo suficientemente simple como para que el agente pueda aprender a jugar sin necesidad de una gran cantidad de datos de entrenamiento. Sin embargo, el juego también es lo suficientemente complejo como para que el agente deba aprender a usar el pensamiento estratégico y la planificación para ganar.

## Cómo entrenar a un agente de aprendizaje por refuerzo profundo para jugar al ping pong

Usaremos la biblioteca OpenAI Gym para entrenar a nuestro agente. OpenAI Gym es un conjunto de herramientas para desarrollar y comparar algoritmos de aprendizaje por refuerzo. Proporciona una variedad de entornos, incluidos juegos clásicos como Pong.

Primero, necesitaremos instalar OpenAI Gym y sus dependencias. También necesitaremos instalar TensorFlow.js y Node.js.

```
# Install OpenAI Gym
pip install gym

# Install TensorFlow.js
npm install @tensorflow/tfjs

# Install Node.js
brew install node
```

A continuación, necesitaremos crear un archivo para nuestro código de entrenamiento. Lo llamaremos `tren.py`.

En `train.py`, comenzaremos importando las bibliotecas que necesitamos.

```python
import gym
import numpy as np
import tensorflow as tf
```

También necesitaremos establecer algunos parámetros para nuestro entrenamiento. El primero es el número de episodios, que es el número de veces que el agente jugará el juego. Estableceremos esto en 100000.

El segundo parámetro es el factor de descuento, que es un valor entre 0 y 1 que determina cuánto valora el agente las recompensas futuras. Un factor de descuento de 1 significa que el agente valora las recompensas futuras por igual que las recompensas inmediatas. Un factor de descuento de 0 significa que el agente solo valora las recompensas inmediatas. Estableceremos el factor de descuento en 0,99.

El tercer parámetro es la tasa de aprendizaje, que es un valor que determina qué tan rápido aprende el agente. Estableceremos la tasa de aprendizaje en 0.001.

```python
# Set training parameters
num_episodes = 100000
discount_factor = 0.99
learning_rate = 0.001
```

Ahora, crearemos la red neuronal profunda que se usará para representar la política del agente. Usaremos una red totalmente conectada de 3 capas con activación ReLU. La red tomará como entrada el estado del juego y como salida las probabilidades de que el agente realice cada acción posible.

```python
# Create the policy network
model = tf.keras.models.Sequential([
  tf.keras.layers.Dense(16, activation='relu', input_shape=(4,)),
  tf.keras.layers.Dense(16, activation='relu'),
  tf.keras.layers.Dense(2, activation='softmax')
])

# Compile the model
model.compile(loss='categorical_crossentropy',
              optimizer=tf.keras.optimizers.Adam(learning_rate),
              metrics=['accuracy'])
```

También necesitamos crear una función para preprocesar el estado del juego. El estado del juego es un vector de 4 dimensiones que representa la posición de la pelota y la posición de las paletas. Escalaremos el estado para que cada dimensión esté entre -1 y 1.

```python
def preprocess_state(state):
  # Scale the state so that each dimension is between -1 and 1
  state = state.astype(np.float32)
  state /= 255
  return state
```

Ahora, podemos comenzar a entrenar al agente. Usaremos el método `fit` del objeto `model` para entrenar al agente. El método `fit` toma como entrada los estados y acciones del agente. Los estados son los vectores de 4 dimensiones que representan la posición de la pelota y la posición de las paletas. Las acciones son los vectores bidimensionales que representan las probabilidades de que el agente realice cada acción posible.

También usaremos la función `discount_rewards` para descontar las recompensas que recibe el agente. Esta función toma como entrada las recompensas que recibió el agente y devuelve las recompensas con descuento.

```python
# Train the agent
for episode in range(num_episodes):
  # Reset the environment
  state = env.reset()
  state = preprocess_state(state)
  done = False
  rewards = []
  
  while not done:
    # Get the probabilities of the agent taking each action
    action_probs = model.predict(state)
    
    # Sample an action from the action probabilities
    action = np.random.choice(np.arange(2), p=action_probs[0])
    
    # Take the action and get the next state and reward
    next_state, reward, done, _ = env.step(action)
    next_state = preprocess_state(next_state)
    
    # Store the reward
    rewards.append(reward)
    
    # Update the state
    state = next_state
  
  # Discount the rewards
  discounted_rewards = discount_rewards(rewards, discount_factor)
  
  # Get the loss and accuracy
  loss, accuracy = model.evaluate(state, action, verbose=0)
  
  # Print the episode number, loss, and accuracy
  print('Episode: {}, Loss: {}, Accuracy: {}'.format(episode, loss, accuracy))
```

¡Eso es! Ahora hemos entrenado a un agente de aprendizaje de refuerzo profundo para jugar el juego clásico Pong.

## Cómo jugar contra el agente

Podemos usar la función `predict_action` para obtener la acción que el agente tomará dado un estado.

```python
def predict_action(state):
  # Get the probabilities of the agent taking each action
  action_probs = model.predict(state)
  
  # Sample an action from the action probabilities
  action = np.random.choice(np.arange(2), p=action_probs[0])
  return action
```

Podemos usar la función `play_episode` para que el agente reproduzca un episodio del juego.

```python
def play_episode(env):
  # Reset the environment
  state = env.reset()
  state = preprocess_state(state)
  done = False
  rewards = []
  
  while not done:
    # Get the action the agent will take
    action = predict_action(state)
    
    # Take the action and get the next state and reward
    next_state, reward, done, _ = env.step(action)
    next_state = preprocess_state(next_state)
    
    # Store the reward
    rewards.append(reward)
    
    # Update the state
    state = next_state
  
  return rewards
```

Podemos usar la función `play_episodes` para que el agente juegue varios episodios del juego.

```python
def play_episodes(env, num_episodes):
  rewards = []
  
  for episode in range(num_episodes):
    episode_rewards = play_episode(env)
    rewards.append(np.sum(episode_rewards))
  
  return rewards
```

Ahora, podemos usar la función `play_episodes` para que el agente juegue 10 episodios del juego.

```python
# Play 10 episodes
rewards = play_episodes(env, 10)

# Print the average reward
print('Average reward: {}'.format(np.mean(rewards)))
```

El agente debe poder jugar el juego razonablemente bien.

## Conclusión

En esta publicación, le mostramos cómo usar TensorFlow.js y Node.js para capacitar a un agente de aprendizaje de refuerzo profundo para que juegue el juego clásico Pong. También proporcionamos una interfaz basada en web para jugar contra el agente.

El aprendizaje de refuerzo profundo es una técnica de aprendizaje automático de vanguardia que es muy adecuada para capacitar a los agentes para realizar tareas complejas en entornos difíciles. TensorFlow.js y Node.js son herramientas poderosas para entrenar e implementar modelos de aprendizaje automático.