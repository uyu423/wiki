---
title: Pygame
description: 
published: true
date: 2023-02-05T05:17:36.024Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:17:34.124Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Pygame***English** document is available*](/en/Knowledge-base/Dictionary/pygame)
{.links-list}

# Pygame

## Descripción general
Pygame es un conjunto de módulos de Python diseñados para escribir videojuegos. Es altamente portátil y se ejecuta en casi todas las plataformas y sistemas operativos. Pygame proporciona funcionalidad como manipulación de sprites, sonido y música, así como soporte para gráficos 2D y 3D.

## Descripción
Pygame es una biblioteca de Python diseñada para crear juegos. Está construido sobre la popular biblioteca SDL. Pygame proporciona un conjunto de módulos de Python diseñados para escribir juegos. Es altamente portátil y se ejecuta en casi todas las plataformas y sistemas operativos.

Pygame proporciona una gama de características útiles para el desarrollo de juegos. Proporciona soporte para gráficos 2D y 3D, así como manipulación de sprites y sonido. También proporciona soporte para controladores de juegos y joysticks.

Pygame es un proyecto de código abierto y es mantenido por un equipo de voluntarios. Se publica bajo la Licencia Pública General Menor de GNU.

## Historia
Pygame fue lanzado por primera vez en 2000 por Pete Shinners. Inicialmente se desarrolló como reemplazo de la antigua biblioteca PySDL. El proyecto ganó popularidad rápidamente y ahora es una de las bibliotecas de desarrollo de juegos más populares para Python.

## Características
Pygame proporciona una gama de características para el desarrollo de juegos. Éstas incluyen:
- Soporte para gráficos 2D y 3D
- Manipulación de sprites y sonido.
- Soporte para controladores de juegos y joysticks
- Soporte para múltiples dispositivos de entrada
- Soporte para redes
- Soporte para múltiples plataformas y sistemas operativos
- Código abierto y de uso gratuito

## Ejemplo
El siguiente ejemplo muestra cómo crear un juego simple usando Pygame:

```python
import pygame

# Initialize pygame
pygame.init()

# Create the screen
screen = pygame.display.set_mode((800, 600))

# Create a clock to control the game's frame rate
clock = pygame.time.Clock()

# Game loop
running = True
while running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Update the game
    # ...

    # Draw the game
    # ...

    # Flip the display
    pygame.display.flip()

    # Delay to get the desired frame rate
    clock.tick(60)

# Quit pygame
pygame.quit()
```

## Pros y contras
### Ventajas
- Fácil de usar
- Altamente portátil
- Código abierto y de uso gratuito
- Soporte para múltiples plataformas y sistemas operativos
- Soporte para redes

### Contras
- Soporte limitado para gráficos 3D
- Soporte limitado para controladores de juegos
- Soporte limitado para redes

## Controversia
Pygame ha sido criticado por su falta de soporte para gráficos 3D y controladores de juegos. Sin embargo, sigue siendo una de las bibliotecas de desarrollo de juegos más populares para Python.

## Tecnología relacionada
Pygame está relacionado con otras bibliotecas de desarrollo de juegos como SDL y OpenGL.

## Digresión
Pygame también se usa con fines educativos, ya que es fácil de aprender y usar.

## Otros
Pygame es una excelente opción para el desarrollo de juegos en Python. Es fácil de usar y muy portátil. Proporciona soporte para gráficos 2D y 3D, así como manipulación de sprites y sonido. También proporciona soporte para controladores de juegos y joysticks.