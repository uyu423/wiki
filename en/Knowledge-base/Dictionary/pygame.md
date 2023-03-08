---
title: Pygame
description: 
published: true
date: 2023-02-05T05:17:40.669Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:17:34.131Z
---

- [Pygame***Japanese** document is available*](/ja/Knowledge-base/Dictionary/pygame)
{.links-list}
- [Pygame***Spanish** document is available*](/es/Knowledge-base/Dictionary/pygame)
{.links-list}
- [Pygame***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/pygame)
{.links-list}
- [Pygame***Korean** document is available*](/ko/Knowledge-base/Dictionary/pygame)
{.links-list}

# Pygame

## Overview
Pygame is a set of Python modules designed for writing video games. It is highly portable and runs on nearly every platform and operating system. Pygame provides functionality such as sprite, sound, and music manipulation, as well as support for 2D and 3D graphics.

## Description
Pygame is a Python library designed for creating games. It is built on top of the popular SDL library. Pygame provides a set of Python modules designed to write games. It is highly portable and runs on almost every platform and operating system.

Pygame provides a range of useful features for game development. It provides support for 2D and 3D graphics, as well as sprite and sound manipulation. It also provides support for game controllers and joysticks.

Pygame is an open source project, and is maintained by a team of volunteers. It is released under the GNU Lesser General Public License.

## History
Pygame was first released in 2000 by Pete Shinners. It was initially developed as a replacement for the aging PySDL library. The project quickly gained popularity, and is now one of the most popular game development libraries for Python.

## Features
Pygame provides a range of features for game development. These include:
- Support for 2D and 3D graphics
- Sprite and sound manipulation
- Support for game controllers and joysticks
- Support for multiple input devices
- Support for networking
- Support for multiple platforms and operating systems
- Open source and free to use

## Example
The following example shows how to create a simple game using Pygame:

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

## Pros and Cons
### Pros
- Easy to use
- Highly portable
- Open source and free to use
- Support for multiple platforms and operating systems
- Support for networking

### Cons
- Limited support for 3D graphics
- Limited support for game controllers
- Limited support for networking

## Controversy
Pygame has been criticized for its lack of support for 3D graphics and game controllers. However, it is still one of the most popular game development libraries for Python.

## Related Technology
Pygame is related to other game development libraries such as SDL and OpenGL.

## Digression
Pygame is also used for educational purposes, as it is easy to learn and use.

## Others
Pygame is a great choice for game development in Python. It is easy to use and highly portable. It provides support for 2D and 3D graphics, as well as sprite and sound manipulation. It also provides support for game controllers and joysticks.