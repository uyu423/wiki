---
title: Pygame
description: 
published: true
date: 2023-02-05T05:17:36.208Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:17:34.123Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Pygame***English** document is available*](/en/Knowledge-base/Dictionary/pygame)
{.links-list}

# 파이게임

## 개요
파이게임은 비디오 게임을 작성하기 위해 설계된 파이썬 모듈 세트입니다. 이식성이 뛰어나고 거의 모든 플랫폼과 운영 체제에서 실행됩니다. 파이게임은 스프라이트, 사운드, 음악 조작과 같은 기능과 2D 및 3D 그래픽 지원을 제공합니다.

## 설명
Pygame은 게임 제작을 위해 설계된 Python 라이브러리입니다. 인기 있는 SDL 라이브러리 위에 구축되었습니다. Pygame은 게임을 작성하도록 설계된 Python 모듈 세트를 제공합니다. 이식성이 뛰어나고 거의 모든 플랫폼과 운영 체제에서 실행됩니다.

파이게임은 게임 개발에 유용한 다양한 기능을 제공합니다. 2D 및 3D 그래픽은 물론 스프라이트 및 사운드 조작을 지원합니다. 또한 게임 컨트롤러와 조이스틱을 지원합니다.

파이게임은 오픈 소스 프로젝트이며 자원봉사자 팀이 관리합니다. GNU Lesser General Public License에 따라 배포됩니다.

## 역사
파이게임은 2000년 Pete Shinners에 의해 처음 출시되었습니다. 처음에는 오래된 PySDL 라이브러리를 대체하기 위해 개발되었습니다. 이 프로젝트는 빠르게 인기를 얻었으며 현재 가장 인기 있는 Python용 게임 개발 라이브러리 중 하나입니다.

## 특징
파이게임은 게임 개발을 위한 다양한 기능을 제공합니다. 여기에는 다음이 포함됩니다.
- 2D 및 3D 그래픽 지원
- 스프라이트 및 사운드 조작
- 게임 컨트롤러 및 조이스틱 지원
- 여러 입력 장치 지원
- 네트워킹 지원
- 여러 플랫폼 및 운영 체제 지원
- 오픈 소스 및 무료 사용

## 예
다음 예제는 Pygame을 사용하여 간단한 게임을 만드는 방법을 보여줍니다.

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

## 장점과 단점
### 장점
- 사용하기 쉬운
- 높은 휴대성
- 오픈 소스 및 무료 사용
- 여러 플랫폼 및 운영 체제 지원
- 네트워킹 지원

### 단점
- 3D 그래픽에 대한 제한된 지원
- 게임 컨트롤러에 대한 제한된 지원
- 네트워킹에 대한 제한된 지원

## 논란
파이게임은 3D 그래픽과 게임 컨트롤러를 지원하지 않는다는 비판을 받아왔다. 그러나 여전히 Python에서 가장 인기 있는 게임 개발 라이브러리 중 하나입니다.

## 관련 기술
파이게임은 SDL 및 OpenGL과 같은 다른 게임 개발 라이브러리와 관련이 있습니다.

## 여담
파이게임은 배우고 사용하기 쉽기 때문에 교육 목적으로도 사용됩니다.

## 기타
파이게임은 파이썬으로 게임을 개발하기 위한 훌륭한 선택입니다. 사용하기 쉽고 휴대성이 뛰어납니다. 2D 및 3D 그래픽은 물론 스프라이트 및 사운드 조작을 지원합니다. 또한 게임 컨트롤러와 조이스틱을 지원합니다.